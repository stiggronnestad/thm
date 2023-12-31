# AoC 2023 - Day 7

> `Log analysis` ‘Tis the season for log chopping!

> To take revenge for the company demoting him to regional manager during the acquisition, Tracy McGreedy installed the CrypTOYminer, a malware he downloaded from the dark web, on all workstations and servers. Even more worrying and unknown to McGreedy, this malware includes a data-stealing functionality, which the malware author benefits from!

## Learning Objectives
> - Revisiting log files and their importance.
> - Understanding what a proxy is and breaking down the contents of a proxy log.
> - Building Linux command-line skills to parse log entries manually.
> - Analysing a proxy log based on typical use cases.

## Steps

Task completed using the split-view online.

I'm tasked to analyze a dataset of logs after a malware attack.

The VM contains the log-file: "/home/ubuntu/Desktop/artefacts/access.log" which is used in this session.

```bash
ubuntu@tryhackme:~$ cd Desktop/artefacts/
ubuntu@tryhackme:~/Desktop/artefacts$ ls -la    
total 8420
drwxrwxr-x 2 ubuntu ubuntu    4096 Oct 27 08:55 .
drwxr-xr-x 3 ubuntu ubuntu    4096 Oct 26 08:09 ..
-rw-r--r-- 1 ubuntu ubuntu 8612364 Oct 27 08:55 access.log
ubuntu@tryhackme:~/Desktop/artefacts$ 
```

The log file follows the following format:

```bash
timestamp - source_ip - domain:port - http_method - http_uri - status_code - response_size - user_agent
```

The `cut` command can be used to parse out specific portions. The following command uses `-d ' '` (1 space delimiter) and outputs columns 1, 3 and 6 from `access.log`.

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cut -d ' ' -f1,3,6 access.log
```

## Question 1

> How many unique IP addresses are connected to the proxy server?

Lets just count the unique IPs from column 2.

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cut -d ' ' -f2 access.log | sort | uniq  
{REDACTED}
```

## Question 2

> How many unique domains were accessed by all workstations?

Lets just fetch the unique domains (cutting the ':' for ports) from column 3 and automatically counting them, theres a few.

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cut -d ' ' -f3 access.log| cut -d ':' -f1 | sort | uniq | wc -l
{REDACTED}
```

## Question 3

> What status code is generated by the HTTP requests to the least accessed domain?

I did this semi-manually, doing a count of the domains I could quickly see that there was only 1 with double digit visits. By manually checking 1 entry in the log file I found the status code.

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cut -d ' ' -f3 access.log| cut -d ':' -f1 | sort | uniq -c
ubuntu@tryhackme:~/Desktop/artefacts$ cat access.log | grep '{REDACTED}' | tail -n 1
{REDACTED}
```

## Question 4

> Based on the high count of connection attempts, what is the name of the suspicious domain?

By checking the most used domains I quickly found one that stood out...

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cut -d ' ' -f3 access.log| cut -d ':' -f1 | sort | uniq -c | sort -n
```

## Question 5

>  What is the source IP of the workstation that accessed the malicious domain?

I just search the logfile for the domain, cut it like before, lookup the ip from column 2 and retrieve the uniqe entries.

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cat access.log | grep '{REDACTED}' | cut -d ' ' -f2 | uniq
{REDACTED}
```

## Question 6

> How many requests were made on the malicious domain in total?

This we know from answering the previous questions.

## Question 7

> Having retrieved the exfiltrated data, what is the hidden flag?

By checking the url parameters for the suspicious traffic I found that the strings might look something like bas64 encoded. Piping them directly into base64 decoding revealed readable data.

```bash
ubuntu@tryhackme:~/Desktop/artefacts$ cat access.log | grep '{REDACTED}' | cut -d ' ' -f5 | uniq
[...]
/storage.php?goodies=b2RlbCBUcmFpbiBTZXQK
[...]

ubuntu@tryhackme:~/Desktop/artefacts$ cat access.log | grep '{REDACTED}' | cut -d ' ' -f5 | uniq | cut -d '=' -f2 | base64 -d
[...]
43d590c8d2f18113310107d93cce0b3a,Mia,Mini Science Microscope
[...]

ubuntu@tryhackme:~/Desktop/artefacts$ cat access.log | grep 'frostlings' | cut -d ' ' -f5 | uniq | cut -d '=' -f2 | base64 -d | grep 'THM'
72703959c91cb18edbefedc692c45204,SOC Analyst,THM{REDACTED}
```