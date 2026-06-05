# Module 9 - State-Machine DP

## Module Goal

Learn how to model each step with a small number of modes and transitions between them.

## Subtopics

- Multiple states per day or index
- Holding vs not holding
- Cooldown states
- Transaction fee states
- Transaction-limit states
- State compression

## Core Pattern

`dp[i][state]` stores the answer at step `i` while being in a specific mode.

## Representative Problems

- LC 121 - Best Time to Buy and Sell Stock
- LC 122 - Best Time to Buy and Sell Stock II
- LC 309 - Best Time to Buy and Sell Stock with Cooldown
- LC 714 - Best Time to Buy and Sell Stock with Transaction Fee

## Status

Queued. We will expand this module after the earlier modules.# Module 9: State-Machine DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers DP where each day or index can be in one of a small number of modes.

## Focus

Learn how to model modes like holding, not holding, cooling down, or having limited transactions left, and then transition cleanly between them.

## Subtopics

- Multiple states per day or index
- Holding vs not holding
- Cooldown states
- Transaction fee states
- Transaction-limit states
- State compression

## Core Pattern

`dp[i][state]` stores the best answer on day or index `i` while being in a specific mode, and transitions switch between modes based on the action taken.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 121 - Best Time to Buy and Sell Stock |
| Must do | LC 122 - Best Time to Buy and Sell Stock II |
| Must do | LC 309 - Best Time to Buy and Sell Stock with Cooldown |
| Must do | LC 714 - Best Time to Buy and Sell Stock with Transaction Fee |
| Good to do | LC 123 - Best Time to Buy and Sell Stock III |
| Stretch | LC 188 - Best Time to Buy and Sell Stock IV |

## How We Will Explore It

We will start by drawing state diagrams and then convert them into compact DP transitions.