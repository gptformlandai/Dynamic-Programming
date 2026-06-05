# Module 11 - DAG and Graph DP

## Module Goal

Learn how to use DFS plus memoization or topological order when states form an acyclic dependency graph.

## Subtopics

- Memoized DFS on DAG-like states
- Topological-order DP
- Longest path on acyclic dependencies
- Matrix path problems that behave like DAGs
- Graph states as DP states

## Core Pattern

Compute each state once using memoization or topological order.

## Representative Problems

- LC 329 - Longest Increasing Path in a Matrix
- LC 2328 - Number of Increasing Paths in a Grid
- LC 2684 - Maximum Number of Moves in a Grid
- LC 1857 - Largest Color Value in a Directed Graph

## Status

Queued. We will expand this module after the earlier modules.# Module 11: DAG and Graph DP

Status: Queued

## Index

- [Overview](#overview)
- [Focus](#focus)
- [Subtopics](#subtopics)
- [Core Pattern](#core-pattern)
- [Representative Problems](#representative-problems)
- [How We Will Explore It](#how-we-will-explore-it)

## Overview

This module covers DP on acyclic dependency graphs, whether the graph is explicit or implicit.

## Focus

Learn how DFS plus memoization and topological order both compute each state once when dependencies are acyclic.

## Subtopics

- Memoized DFS on DAG-like states
- Topological-order DP
- Longest path on acyclic dependencies
- Matrix path problems that behave like DAGs
- Graph states as DP states

## Core Pattern

Compute each state once using DFS plus memoization or topological order, depending on whether the dependency graph is implicit or explicit.

## Representative Problems

| Priority | Problem |
| --- | --- |
| Must do | LC 329 - Longest Increasing Path in a Matrix |
| Good to do | LC 2328 - Number of Increasing Paths in a Grid |
| Good to do | LC 2684 - Maximum Number of Moves in a Grid |
| Stretch | LC 1857 - Largest Color Value in a Directed Graph |

## How We Will Explore It

We will start from implicit DAGs hidden inside matrix problems and then move to explicit graph states.