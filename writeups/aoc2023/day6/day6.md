# AoC 2023 - Day 6

> `Memory Corruption` Memories of Christmas Past

## Learning Objectives
> - Understand how specific languages may not handle memory safely.
> - Understand how variables might overflow into adjacent memory and corrupt it.
> - Exploit a simple buffer overflow to directly change memory you are not supposed to access.

## Steps

```bash
└─$ export box=10.10.98.105
└─$ firefox $box
```

The website contains a game with some fun buffer-overflow-issues. The goal is to gain a `star` which can be put on the christmas tree.

## Question 1

> If the coins variable had the in-memory value in the image below, how many coins would you have in the game?

Using an online-tool for converting between `HEX` and `DEC`. Remember to use `little-endian`...

## Question 2

> What is the value of the final flag?

Given when placing the `star` on the tree. The `star` can't be bought, but the inventory is also part of the memory...