# Module 8 - LIS and Transition-Heavy DP

## Module Goal

Learn how to handle states that can transition from many earlier valid states.

## Subtopics

- Transition from all previous valid states
- `O(n^2)` LIS reasoning
- Counting LIS variants
- Chain-building DP
- Partition DP with variable previous cut
- LIS optimization with binary search

## Core Pattern

`dp[i]` stores the best answer ending at index `i`, and valid transitions may come from many earlier indices.

## Representative Problems

- LC 300 - Longest Increasing Subsequence
- LC 673 - Number of Longest Increasing Subsequence
- LC 1048 - Longest String Chain
- LC 1043 - Partition Array for Maximum Sum

## Status

Queued. We will expand this module after the earlier modules.# Module 8: LIS and Transition-Heavy DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers problems where a state can transition from many earlier valid states rather than a fixed small set.

## Focus

Learn LIS-style transitions, partition-based transitions, chain-building, and the difference between full DP reasoning and LIS-specific optimization tricks.

## Subtopics

- Transition from all previous valid states
- `O(n^2)` LIS reasoning
- Counting LIS variants
- Chain-building DP
- Partition DP with variable previous cut
- LIS optimization with binary search

## Core Pattern

`dp[i]` stores the best answer ending at index `i`, and transitions may come from every earlier index `j` that satisfies a validity condition.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 300 - Longest Increasing Subsequence |
| Must do | LC 673 - Number of Longest Increasing Subsequence |
| Must do | LC 1048 - Longest String Chain |
| Good to do | LC 1043 - Partition Array for Maximum Sum |
| Good to do | LC 1105 - Filling Bookcase Shelves |
| Good to do | LC 813 - Largest Sum of Averages |
| Good to do | LC 1395 - Count Number of Teams |

## How We Will Explore It

We will build this from basic LIS thinking into more general transition-heavy prefix and chain problems.