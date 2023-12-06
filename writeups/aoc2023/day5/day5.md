# AoC 2023 - Day 5

> `Reverse Engineering` A Christmas DOScovery: Tapes of Yule-tide Past

## Learning Objectives
> - Experience how to navigate an unfamiliar legacy system.
> - Learn about DOS and its connection to its contemporary, the Windows Command Prompt.
> - Discover the significance of file signatures and magic bytes in data recovery and file system analysis.

## Magic Bytes

A table of magic bytes refering to the file signature of different files are outlined.

File Format				    | Magic Bytes			    | ASCII representation
----------------------------|---------------------------|----------------------
PNG image file              | 89 50 4E 47 0D 0A 1A 0A	| %PNG
GIF image file              | 47 49 46 38               | GIF8
Windows and DOS executables | 4D 5A	                    | MZ
Linux ELF executables       | 7F 45 4C 46               | .ELF
MP3 audio file              | 49 44 33                  | ID3

## Steps

Using the `DOX-BOX` on the VM.

```bash
EDIT C:\AC2023.BAK
```

The magic bytes of this file is `XX`.

Converting from `XX` (hex) to ASCII using cyberchef gives `AC`.

Replace the `XX` of the backup file and run the `BUMASTER.EXE` tool.

```bash
BUMASTER.EXE C:\AC2023.BAK
```

## Question 1

> How large (in bytes) is the AC2023.BAK file?

Can be read using `dir` in the correct folder.

## Question 2

> What is the name of the backup program?

The name of the backup program is written inside a certain readme file...

## Question 3

> What should the correct bytes be in the backup's file signature to restore the backup properly?

'AC' as HEX.

## Question 4

> What is the flag after restoring the backup successfully?

Given when running the restore tool.