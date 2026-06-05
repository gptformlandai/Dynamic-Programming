# Module 6 - Two-Sequence String DP

## Module Goal

Learn prefix-vs-prefix DP over two strings or two sequences.

## Subtopics

- Prefix-vs-prefix state
- Match vs mismatch transitions
- Longest common subsequence pattern
- Edit-distance pattern
- Subsequence counting
- Interleaving and alignment
- Base row and base column setup

## Core Pattern

`dp[i][j]` represents the answer for the first `i` items of one sequence and the first `j` of another.

## Representative Problems

- LC 1143 - Longest Common Subsequence
- LC 72 - Edit Distance
- LC 115 - Distinct Subsequences
- LC 97 - Interleaving String

## Status

Queued. We will expand this module after the earlier modules.# Module 6: Two-Sequence String DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers problems where the state depends on prefixes of two strings or two sequences.

## Focus

Learn prefix-vs-prefix state design, match and mismatch transitions, base rows and columns, and the main LCS and edit-distance families.

## Subtopics

- Prefix-vs-prefix state
- Match vs mismatch transitions
- Longest common subsequence pattern
- Edit-distance pattern
- Subsequence counting
- Interleaving and alignment
- Base row and base column setup

## Core Pattern

`dp[i][j]` represents the answer for the first `i` characters or elements of one sequence and the first `j` of another.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 1143 - Longest Common Subsequence |
| Must do | LC 72 - Edit Distance |
| Must do | LC 115 - Distinct Subsequences |
| Must do | LC 97 - Interleaving String |
| Good to do | LC 1035 - Uncrossed Lines |
| Good to do | LC 712 - Minimum ASCII Delete Sum for Two Strings |
| Good to do | LC 1092 - Shortest Common Supersequence |
| Good to do | LC 718 - Maximum Length of Repeated Subarray |

## How We Will Explore It

We will build this module from LCS-style matching to edit operations and counting variants.