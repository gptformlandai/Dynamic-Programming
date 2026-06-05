# Module 2 - 1D Linear and Prefix DP

## Module Goal

Learn how to define `dp[i]` for linear sequences, prefixes, and skip-ahead transitions.

## Subtopics

- Prefix DP
- Count, min, max, and boolean forms
- Fixed-lookback transitions
- Variable jump or window transitions
- Prefix segmentation on strings
- Rolling-state optimization

## Core Pattern

`dp[i]` stores the answer for position or prefix `i`, and transitions come from earlier valid positions or cuts.

## Representative Problems

- LC 91 - Decode Ways
- LC 139 - Word Break
- LC 983 - Minimum Cost For Tickets
- LC 2140 - Solving Questions With Brainpower

## Status

Queued. We will expand this module after Module 1.# Module 2: 1D Linear and Prefix DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers problems where one linear state captures the answer for a prefix, suffix, or position.

## Focus

Learn when `dp[i]` is enough, how to classify the result as count, min, max, or boolean, and how to build transitions from earlier positions or valid cuts.

## Subtopics

- Prefix DP
- Count, min, max, and boolean forms
- Fixed-lookback transitions
- Variable jump or window transitions
- Prefix segmentation on strings
- Rolling-state optimization

## Core Pattern

`dp[i]` stores the answer for position or prefix `i`, and transitions come from a small set of earlier positions or valid cuts.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 91 - Decode Ways |
| Must do | LC 139 - Word Break |
| Must do | LC 983 - Minimum Cost For Tickets |
| Must do | LC 2140 - Solving Questions With Brainpower |

## How We Will Explore It

We will take each subtopic one by one, just like Module 1, and expand it into detailed notes, intuition, and exercises.