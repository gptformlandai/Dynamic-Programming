# Module 10 - Tree DP

## Module Goal

Learn how to compute answers over subtrees where parent decisions affect child choices.

## Subtopics

- Subtree answers
- Postorder traversal
- Include or exclude node logic
- Parent-child dependency handling
- Two-state node DP

## Core Pattern

`dp[node][state]` stores the answer for a subtree under a condition.

## Representative Problems

- LC 337 - House Robber III
- LC 968 - Binary Tree Cameras
- LC 834 - Sum of Distances in Tree

## Status

Queued. We will expand this module after the earlier modules.# Module 10: Tree DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers DP over rooted trees where parent and child decisions interact.

## Focus

Learn subtree state design, postorder traversal, include-or-exclude logic, and how to return structured results from children.

## Subtopics

- Subtree answers
- Postorder traversal
- Include or exclude node logic
- Parent-child dependency handling
- Two-state node DP

## Core Pattern

`dp[node][state]` stores the answer for the subtree rooted at `node` under a condition such as taking or not taking the node.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 337 - House Robber III |
| Must do | LC 968 - Binary Tree Cameras |
| Stretch | LC 834 - Sum of Distances in Tree |

## How We Will Explore It

We will begin with postorder thinking and then move to rerooting-aware extensions.