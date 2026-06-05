# Module 5 - Grid DP

## Module Goal

Learn how to define cell-based states and move through matrix dependencies correctly.

## Subtopics

- Path counting
- Minimum or maximum path sum
- Obstacles and blocked cells
- Right and down traversal
- Reverse traversal when required
- Falling-path transitions
- Square-building DP
- Boundary initialization and padding

## Core Pattern

`dp[r][c]` stores the answer for cell `(r, c)` using allowed predecessor cells.

## Representative Problems

- LC 62 - Unique Paths
- LC 63 - Unique Paths II
- LC 64 - Minimum Path Sum
- LC 120 - Triangle

## Status

Queued. We will expand this module after the earlier modules.# Module 5: Grid DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers problems where each DP state is attached to a grid cell.

## Focus

Learn path counting, path optimization, boundary initialization, direction of traversal, and local-square recurrences.

## Subtopics

- Path counting
- Minimum or maximum path sum
- Obstacles and blocked cells
- Right and down traversal
- Reverse traversal when required
- Falling-path transitions
- Square-building DP
- Boundary initialization and padding

## Core Pattern

`dp[r][c]` stores the answer for cell `(r, c)`, using information from allowed predecessor cells.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 62 - Unique Paths |
| Must do | LC 63 - Unique Paths II |
| Must do | LC 64 - Minimum Path Sum |
| Must do | LC 120 - Triangle |
| Good to do | LC 931 - Minimum Falling Path Sum |
| Good to do | LC 221 - Maximal Square |
| Good to do | LC 1277 - Count Square Submatrices with All Ones |
| Stretch | LC 174 - Dungeon Game |

## How We Will Explore It

We will go from simple right-down grids to reverse-direction and local-shape problems.