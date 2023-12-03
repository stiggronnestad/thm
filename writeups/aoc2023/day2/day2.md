# AoC 2023 - Day 2

> `Log Analysis` O Data, All Ye Faithful

## Learning Objectives
> - Get an introduction to what data science involves and how it can be applied in Cybersecurity
> - Get a gentle (We promise) introduction to Python
> - Get to work with some popular Python libraries such as Pandas and Matplotlib to crunch data
> - Help McHoneyBell establish an understanding of AntarctiCrafts’ network

## Notes
This task involves keywords like `log analysis`, `data science` and `jupyter`. I have used Python extensively in the past, but never used `jupyter`, so let's see what this is all about.

I get a quick introduction to:
- Python
- Pandas
- Matplotlib


## Question 1

> How many packets were captured (looking at the PacketNumber)?

This can be done by static analysis of the `network_traffic.csv`.

## Question 2

> What IP address sent the most amount of traffic during the packet capture?

Here we can group by `Source` and count the result.

```python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('network_traffic.csv')
df.groupby("Source")["PacketNumber"].nunique().idxmax()
```

## Question 3

> What was the most frequent protocol?

Here we just do the same thing, but group by `Protocol`.

```python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_csv('network_traffic.csv')
df.groupby("Protocol")["PacketNumber"].nunique().idxmax()
```