# AoC 2023 - Day 9

> `Malware analysis` She sells C# shells by the C2shore

> Having retrieved the deleted version of the malware that allows Tracy McGreedy to control elves remotely, Forensic McBlue and his team have started investigating to stop the mind control incident. They are now planning to take revenge by analysing the C2's back-end infrastructure based on the malware's source code.

## Learning Objectives
> - The foundations of analysing malware samples safely
> - The fundamentals of .NET binaries
> - The dnSpy tool for decompiling malware samples written in .NET
> - Building an essential methodology for analysing malware source code

## Steps

Task completed using the split-view online.

I'm tasked with handling some malware, let's see what happens.

Using `dnSpy` I can open `JuicyTomaTOY_defanged`, a .Net executable.

Questions will be answered based on the decompiled code from `dnSpy`.

## Question 1

> What HTTP User-Agent was used by the malware for its connection requests to the C2 server?

Both `Getit` and `Postit` functions contains this key.

## Question 2

> What is the HTTP method used to submit the command execution output?

Standard HTTP method for POSTing data.

## Question 3

> What key is used by the malware to encrypt or decrypt the C2 data?

Both `Decryptor` and `Encryptor` contains this key.

## Question 4

> What is the first HTTP URL used by the malware?

Inside `Main` the first URL string is concatenated.

## Question 5

> How many seconds is the hardcoded value used by the sleep function?

The sleep timer is inside `Main`.

## Question 6

> What is the C2 command the attacker uses to execute commands via cmd.exe?

The command parsing is inside `Main`.

## Question 7

> What is the domain used by the malware to download another binary?

The URL is found inside `Main` at the `implant` block.