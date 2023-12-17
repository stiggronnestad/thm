# AoC 2023 - Day 16

> `Machine learning` Can't CAPTCHA this Machine!

> After the great success of using machine learning to detect defective toys and phishing emails, McSkidy is looking to you to help him build a custom brute force script that will make use of ML to solve the CAPTCHA and continue with the brute force attack. There is, however, a bit of irony in having a machine solve a challenge specifically designed to tell humans apart from computers.

## Learning Objectives
> - Complex neural network structures
> - How does a convolutional neural networks function?
> - Using neural networks for optical character recognition
> - Integrating neural networks into red team tooling

## Steps

Task completed using the split-view online. This is a straight walk-through like day 16, but this time as a `read team` member.

## Question 1

> What key process of training a neural network is taken care of by using a CNN?

feature extraction

## Question 2

> What is the name of the process used in the CNN to extract the features?

convolution

## Question 3

> What is the name of the process used to reduce the features down?

pooling

## Question 4

> What off-the-shelf CNN did we use to train a CAPTCHA-cracking OCR model?

Attention OCR

## Question 5

> What is the password that McGreedy set on the HQ Admin portal?

Cracked at the last step in the tutorial.

```bash
cd ~/Desktop/bruteforcer && python3 bruteforce.py
```

## Question 6

> What is the value of the flag that you receive when you successfully authenticate to the HQ Admin portal?

Gained after logging in to `http://hqadmin.thm:8000/`.