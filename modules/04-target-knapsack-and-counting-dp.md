# Module 4 - Target Knapsack and Counting DP

## Module Goal

Learn how to build DP over target sums, capacities, and counting states.

## Subtopics

- 0/1 knapsack
- Unbounded knapsack
- Subset sum
- Partition DP
- Min-coin DP
- Count-ways DP
- Boolean feasibility DP
- Order matters vs order does not matter
- Forward vs reverse loop order

## Core Pattern

Use `dp[target]` or `dp[i][cap]` to track feasibility, optimization, or number of ways.

## Representative Problems

- LC 322 - Coin Change
- LC 518 - Coin Change II
- LC 416 - Partition Equal Subset Sum
- LC 494 - Target Sum

## Status

Queued. We will expand this module after the earlier modules.# Module 4: Target Knapsack and Counting DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers DP over target sums, capacities, feasibility, and number-of-ways states.

## Focus

Learn the difference between 0/1 and unbounded choices, feasibility vs counting vs optimization, and why loop order changes meaning.

## Subtopics

- 0/1 knapsack
- Unbounded knapsack
- Subset sum
- Partition DP
- Min-coin DP
- Count-ways DP
- Boolean feasibility DP
- Order matters vs order does not matter
- Forward vs reverse loop order

## Core Pattern

`dp[target]` or `dp[i][cap]` tracks whether a target is reachable, the minimum or maximum value for it, or the number of ways to build it.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 322 - Coin Change |
| Must do | LC 518 - Coin Change II |
| Must do | LC 416 - Partition Equal Subset Sum |
| Must do | LC 494 - Target Sum |
| Good to do | LC 377 - Combination Sum IV |
| Good to do | LC 279 - Perfect Squares |
| Good to do | LC 474 - Ones and Zeroes |
| Good to do | LC 1049 - Last Stone Weight II |
| Stretch | LC 1155 - Number of Dice Rolls With Target Sum |
| Stretch | LC 879 - Profitable Schemes |

## How We Will Explore It

We will separate the module into clear subfamilies so the same target-state idea does not blur into one big bucket.