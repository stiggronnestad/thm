# AoC 2023 - Day 8

> `Disk forensics` Have a Holly, Jolly Byte!

> The drama unfolds as the Best Festival Company and AntarctiCrafts merger wraps up! Tracy McGreedy, now a grumpy regional manager, secretly plans sabotage. His sidekick, Van Sprinkles, hesitantly kicks off a cyber attack – but guess what? Van Sprinkles is having second thoughts and helps McSkidy's team bust McGreedy's evil scheme!

## Learning Objectives
> - Analyse digital artefacts and evidence.
> - Recover deleted digital artefacts and evidence.
> - Verify the integrity of a drive/image used as evidence.

## Steps

Task completed using the split-view online.

I'm tasked with investigating a malicius USB flash drive that was plugged into `Van Jollys` laptop using `FTK Imager`, this seems like a fun one.

The USB drive is called `Ckr3Ts4uC3` - SecretSauce?

The task was completed using the `FTK Imager` software.

## Question 1

> What is the malware C2 server?

I found this by clicking around the `Evidence Tree` and finding `secretchat.txt`. This is a conversation between `Gr33dYsH4d0W` and `V4nd4LmUffL3r5`.

## Question 2

> What is the file inside the deleted zip archive?

Files marked with an X are deleted, they can still be investigated.

## Question 3

> What flag is hidden in one of the deleted PNG files?

I can search for strings in one of the two `.png` files found on the drive. I did this in hex mode by converting `THM` to hex and searching for the hex codes.

## Question 4

> What is the SHA1 hash of the physical drive and forensic image?

Run Drive/Image verification to get the hash.