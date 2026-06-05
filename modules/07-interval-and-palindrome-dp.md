# Module 7 - Interval and Palindrome DP

## Module Goal

Learn how to define DP on ranges such as subarrays and substrings.

## Subtopics

- Interval state `dp[l][r]`
- Solve by increasing length
- Split-at-`k` transitions
- Shrink-from-both-ends transitions
- Merge-cost DP
- Palindrome interval DP

## Core Pattern

`dp[l][r]` stores the answer for interval `[l, r]` using smaller intervals.

## Representative Problems

- LC 647 - Palindromic Substrings
- LC 516 - Longest Palindromic Subsequence
- LC 312 - Burst Balloons
- LC 664 - Strange Printer

## Status

Queued. We will expand this module after the earlier modules.# Module 7: Interval and Palindrome DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers problems where the natural state is a subarray or substring interval.

## Focus

Learn how to define `dp[l][r]`, iterate by length, split at `k`, and reason from both ends of a range.

## Subtopics

- Interval state `dp[l][r]`
- Solve by increasing length
- Split-at-`k` transitions
- Shrink-from-both-ends transitions
- Merge-cost DP
- Palindrome interval DP

## Core Pattern

`dp[l][r]` stores the answer for interval `[l, r]`, and transitions depend on smaller intervals inside it.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 647 - Palindromic Substrings |
| Must do | LC 516 - Longest Palindromic Subsequence |
| Must do | LC 312 - Burst Balloons |
| Good to do | LC 5 - Longest Palindromic Substring |
| Good to do | LC 1130 - Minimum Cost Tree From Leaf Values |
| Good to do | LC 664 - Strange Printer |
| Stretch | LC 1000 - Minimum Cost to Merge Stones |
| Stretch | LC 1690 - Stone Game VII |

## How We Will Explore It

We will start with range definition and traversal order, then move to split-based interval DP.