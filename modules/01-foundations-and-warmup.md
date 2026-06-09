# Module 1 - Foundations and Warmup

## Index

- [Module Goal](#module-goal)
- [Subtopic Queue](#subtopic-queue)
- [Subtopic 1 - Recursion Basics](#subtopic-1---recursion-basics)
- [Head Recursion vs Tail Recursion](#head-recursion-vs-tail-recursion)
- [Practice for This Subtopic](#practice-for-this-subtopic)
- [Exit Criteria](#exit-criteria)
- [Next Subtopics](#next-subtopics)

## Module Goal

Build the core DP workflow before touching larger patterns.

By the end of this module, you should be able to:

- explain recursion clearly
- spot overlapping subproblems
- justify when DP is valid
- move from recursion to memoization
- move from memoization to tabulation
- reason about base cases and complexity

## Subtopic Queue

1. Recursion basics
2. Overlapping subproblems
3. Optimal substructure
4. Memoization with arrays or maps
5. Tabulation order
6. Base cases and boundary handling
7. Time and space complexity awareness

Current focus: `Recursion basics`

## Subtopic 1 - Recursion Basics

### Intuition

Recursion means solving a problem by asking a smaller version of the same problem to solve itself first.

The whole idea is:

- reduce the problem size
- stop at a simple base case
- build the answer while returning back up

For DP, recursion is the cleanest place to discover the state and the transition before optimizing anything.

### What Recursion Really Needs

Every recursive solution needs exactly two things:

1. A base case
2. A rule that reduces the problem to a smaller state

If either one is missing, recursion breaks.

### Simple Mental Model

Think of recursion as a chain of function calls going down to the simplest case and then returning answers upward.

Example idea:

- to compute `f(4)`
- you may need `f(3)` and `f(2)`
- to compute `f(3)` you may need `f(2)` and `f(1)`
- this keeps shrinking until a base case is reached

This is exactly where DP starts becoming useful, because repeated calls like `f(2)` show up again and again.

### Why This Matters for DP

Most DP problems are easiest to understand in this order:

1. Write the brute-force recursive idea
2. Notice repeated states
3. Cache repeated states with memoization
4. Convert the same logic into tabulation

If recursion is shaky, DP will feel like memorizing formulas.

### Generic Recursive Template

```text
solve(state):
    if state is a base case:
        return base answer

    answer = combine(solve(smaller_state_1), solve(smaller_state_2), ...)
    return answer
```

### Head Recursion vs Tail Recursion

This distinction matters because it changes when the current function does its work.

- Head recursion: the recursive call happens first, and the current call does useful work while the stack is unwinding.
- Tail recursion: the current call finishes all useful work before making the recursive call, so the recursive call is the last operation.

Simple rule to remember:

- If you need to do something after the recursive call returns, that is usually head recursion.
- If you can pass everything needed into the next call and return its answer directly, that is usually tail recursion.

In theory, tail recursion can be optimized into iteration by some languages or compilers. Java and Python do not guarantee tail-call optimization, so tail recursion here is mainly a thinking tool for writing cleaner state transitions.

#### 1. Print 1 to n

This is the easiest place to feel the difference.

- In head recursion, you go deeper first and print while coming back.
- In tail recursion, you print now and then move to the next call.

Head recursion prints in ascending order only if you recurse down to `1` first and print on the way back.

```java
class PrintOneToN {
   static void printHead(int n) {
      if (n == 0) {
         return;
      }
      printHead(n - 1);
      System.out.print(n + " ");
   }

   static void printTail(int current, int n) {
      if (current > n) {
         return;
      }
      System.out.print(current + " ");
      printTail(current + 1, n);
   }
}
```

```python
def print_head(n: int) -> None:
   if n == 0:
      return
   print_head(n - 1)
   print(n, end=" ")


def print_tail(current: int, n: int) -> None:
   if current > n:
      return
   print(current, end=" ")
   print_tail(current + 1, n)
```

Why these are different:

- `printHead(n)` delays the print until smaller calls finish.
- `printTail(current, n)` does the print before the recursive call, so no work is left after recursion.

#### 2. Factorial

Factorial is a strong example because the normal textbook version is head recursion, but it converts neatly into tail recursion by carrying the running product.

Head-recursive idea:

```text
fact(n) = n * fact(n - 1)
```

Tail-recursive idea:

```text
fact(n, acc) = fact(n - 1, acc * n)
```

```java
class FactorialExamples {
   static int factorialHead(int n) {
      if (n <= 1) {
         return 1;
      }
      return n * factorialHead(n - 1);
   }

   static int factorialTail(int n) {
      return factorialTailHelper(n, 1);
   }

   static int factorialTailHelper(int n, int acc) {
      if (n <= 1) {
         return acc;
      }
      return factorialTailHelper(n - 1, acc * n);
   }
}
```

```python
def factorial_head(n: int) -> int:
   if n <= 1:
      return 1
   return n * factorial_head(n - 1)


def factorial_tail(n: int, acc: int = 1) -> int:
   if n <= 1:
      return acc
   return factorial_tail(n - 1, acc * n)
```

What changed:

- In the head version, multiplication happens after the recursive call returns.
- In the tail version, the multiplication is done before the next call, and the partial answer is stored in `acc`.

#### 3. Fibonacci

Fibonacci is important because the usual recursive version is not tail recursive and also repeats work heavily.

Head-recursive idea:

```text
fib(n) = fib(n - 1) + fib(n - 2)
```

This is a classic branching recursion. After the calls return, the current call still has to add them, so it is not tail recursion.

To make Fibonacci tail recursive, we change the state. Instead of asking only for `fib(n)`, we carry the last two Fibonacci values forward.

```java
class FibonacciExamples {
   static int fibonacciHead(int n) {
      if (n <= 1) {
         return n;
      }
      return fibonacciHead(n - 1) + fibonacciHead(n - 2);
   }

   static int fibonacciTail(int n) {
      return fibonacciTailHelper(n, 0, 1);
   }

   static int fibonacciTailHelper(int n, int a, int b) {
      if (n == 0) {
         return a;
      }
      return fibonacciTailHelper(n - 1, b, a + b);
   }
}
```

```python
def fibonacci_head(n: int) -> int:
   if n <= 1:
      return n
   return fibonacci_head(n - 1) + fibonacci_head(n - 2)


def fibonacci_tail(n: int, a: int = 0, b: int = 1) -> int:
   if n == 0:
      return a
   return fibonacci_tail(n - 1, b, a + b)
```

Why this matters for DP thinking:

- The head version exposes the recurrence clearly, so it is good for learning DP.
- The tail version shows that sometimes you can redesign the state to carry exactly what the next step needs.

#### 4. Steps and Stairs Problems

For the common stairs problem, `ways(n)` means the number of ways to reach step `n` when you can take 1 or 2 steps.

Head-recursive form:

```text
ways(n) = ways(n - 1) + ways(n - 2)
```

That form is best for discovering the DP recurrence, but it repeats states just like Fibonacci.

For a tail-recursive version, carry the last two answers forward:

- if you know `ways(i)` and `ways(i + 1)`
- then the next pair becomes `ways(i + 1)` and `ways(i) + ways(i + 1)`

```java
class StairsExamples {
   static int stairsHead(int n) {
      if (n <= 1) {
         return 1;
      }
      return stairsHead(n - 1) + stairsHead(n - 2);
   }

   static int stairsTail(int n) {
      return stairsTailHelper(n, 1, 1);
   }

   static int stairsTailHelper(int remaining, int currentWays, int nextWays) {
      if (remaining == 0) {
         return currentWays;
      }
      return stairsTailHelper(remaining - 1, nextWays, currentWays + nextWays);
   }
}
```

```python
def stairs_head(n: int) -> int:
   if n <= 1:
      return 1
   return stairs_head(n - 1) + stairs_head(n - 2)


def stairs_tail(remaining: int, current_ways: int = 1, next_ways: int = 1) -> int:
   if remaining == 0:
      return current_ways
   return stairs_tail(remaining - 1, next_ways, current_ways + next_ways)
```

How to interpret the tail state:

- `currentWays` is the answer for the current stair count.
- `nextWays` is the answer for the next stair count.
- Each recursive step shifts the window forward by one stair.

#### When to prefer each style

- Prefer head recursion when you are trying to discover the recurrence relation from the problem statement.
- Prefer tail recursion when a running result or a small rolling state can fully describe the remaining work.
- For DP interviews, write the head-recursive recurrence first because it makes overlapping subproblems visible.
- For implementation, iteration is often better than either form in Java and Python when depth can grow large.

#### Final takeaway

Head recursion is better for learning the structure of a problem.

Tail recursion is better for learning how to carry state forward without doing extra work after the recursive call.

For DP, both are useful:

- head recursion helps you discover the recurrence
- tail recursion helps you think about state compression and iterative conversion

### Tiny Example: Climbing Stairs

Problem idea: to reach stair `n`, you can come from `n - 1` or `n - 2`.

Recursive definition:

```text
ways(n) = ways(n - 1) + ways(n - 2)
```

Base cases:

- `ways(0) = 1`
- `ways(1) = 1`

What this teaches you:

- the state is `n`
- the transition comes from smaller states
- repeated calls will appear naturally

### What to Look for While Writing Recursion

When you write a recursive solution, force yourself to answer these questions:

1. What is the state?
2. What makes the problem smaller?
3. What are the base cases?
4. What values need to be combined?
5. Does the same state appear multiple times?

### Common Mistakes

- Missing base cases
- Base cases that return the wrong value
- Recursive calls that do not shrink the state
- Using recursion without being able to define the state cleanly
- Jumping to tabulation before understanding the recursion

### Subtopic Summary

Recursion is not DP by itself. It is the discovery layer for DP.

If you can define the recursive state and transition clearly, memoization and tabulation become much easier.

## Practice for This Subtopic

Solve these in order:

1. LC 509 - Fibonacci Number
2. LC 70 - Climbing Stairs
3. LC 1137 - N-th Tribonacci Number
4. LC 746 - Min Cost Climbing Stairs

For each problem, write these five lines before coding:

1. State
2. Transition
3. Base case
4. Time complexity of brute force
5. Where repeated states appear

## Exit Criteria

Do not move to the next subtopic until you can do all of this without notes:

- explain recursion in one clean sentence
- identify the base case immediately
- write a smaller-state recurrence
- trace a small recursive call tree by hand
- point out repeated states in that tree

## Next Subtopics

- Overlapping subproblems: identify repeated states and why caching helps
- Optimal substructure: understand when smaller optimal answers combine into a larger one
- Memoization with arrays or maps: store computed states and avoid recomputation
- Tabulation order: decide which state must be computed before another
- Base cases and boundary handling: prevent off-by-one and invalid state errors
- Time and space complexity awareness: compare brute force, memoized, and tabulated forms# Module 1: Foundations and Warmup

Status: Active

## Index

- [Module Overview](#module-overview)
- [Learning Goals](#learning-goals)
- [Subtopic Tracker](#subtopic-tracker)
- [Subtopic 1 - Recursion Basics](#subtopic-1---recursion-basics)
- [Practice Set](#practice-set)
- [Checkpoint Questions](#checkpoint-questions)
- [Next Up](#next-up)

## Module Overview

This module builds the mental model that every later DP problem relies on. The goal is not to memorize formulas. The goal is to learn how to break a problem into smaller states, solve the smallest version first, and trust that bigger answers are built from smaller ones.

## Learning Goals

- Understand what recursion is doing under the hood.
- Learn how a recursive function shrinks a problem.
- Recognize the difference between the state, the choices, and the final answer.
- Get comfortable writing base cases before transitions.
- Prepare for the next step: spotting repeated recursive work and turning it into DP.

## Subtopic Tracker

| Order | Subtopic | Status |
| --- | --- | --- |
| 1 | Recursion basics | Active |
| 2 | Overlapping subproblems | Pending |
| 3 | Optimal substructure | Pending |
| 4 | Memoization with arrays or maps | Pending |
| 5 | Tabulation order | Pending |
| 6 | Base cases and boundary handling | Pending |
| 7 | Time and space complexity awareness | Pending |

## Subtopic 1 - Recursion Basics

### What recursion means

Recursion is a way of solving a problem by asking the same problem on a smaller input until you reach a version that is small enough to answer directly.

In plain words:

- A function calls itself.
- Each call moves toward a smaller problem.
- A base case stops the process.

### Why recursion matters before DP

Dynamic Programming usually starts as recursion. Before you can write `dp[i]`, you need to understand what smaller problem `i` depends on.

Recursion gives you that first draft.

Without recursion, beginners often try to jump straight to a table and end up memorizing patterns instead of understanding them.

### The three parts of a recursive solution

1. State
   What input uniquely describes the current problem?

2. Base case
   What is the smallest input you can answer immediately?

3. Recurrence
   How do you reduce the current problem to smaller problems?

### The mental model to use

When you see a problem, ask these questions in order:

1. What does one function call represent?
2. What is the smallest version of this problem?
3. If I knew the answers to smaller versions, how would I build the current answer?

That is the bridge from recursion to DP.

### Example 1: Fibonacci

If `fib(n)` means the `n`th Fibonacci number, then:

- State: `n`
- Base case: `fib(0) = 0`, `fib(1) = 1`
- Recurrence: `fib(n) = fib(n - 1) + fib(n - 2)`

```text
fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)
```

This is the cleanest recursion example because it shows the full idea with almost no extra details.

### Example 2: Climbing Stairs

If `ways(n)` means the number of ways to reach step `n`, then the final move was either:

- a jump from `n - 1`
- a jump from `n - 2`

So:

- State: current step `n`
- Base case: `ways(0) = 1`, `ways(1) = 1`
- Recurrence: `ways(n) = ways(n - 1) + ways(n - 2)`

The important part is not the formula itself. The important part is how you derived it from the last move.

### What recursion teaches you for DP

- How to define a state.
- How to find smaller subproblems.
- How to write a valid recurrence.
- Why base cases are not optional.
- Why some recursive solutions explode in time when the same state is recomputed many times.

That last point leads directly into the next subtopic: overlapping subproblems.

### Common mistakes

1. Missing base cases
   The function never stops or returns wrong answers for small inputs.

2. Wrong state definition
   The function parameters do not fully describe the problem.

3. Shrinking the problem incorrectly
   The recursive calls do not move toward the base case.

4. Mixing index meaning
   Sometimes `n` means length, sometimes it means index. Pick one meaning and stay consistent.

5. Blindly copying recurrence patterns
   You should derive the recurrence from the problem story, not guess it from memory.

### What to write in an interview

Before coding, say this out loud:

- My state is `...`
- My base case is `...`
- From this state, I have these choices: `...`
- That gives me this recurrence: `...`

If you can say those four lines clearly, your DP setup is usually on the right track.

## Practice Set

| Priority | Problem | What to focus on |
| --- | --- | --- |
| Must do | LC 509 - Fibonacci Number | state, base case, recurrence |
| Must do | LC 70 - Climbing Stairs | derive recurrence from last move |
| Good to do | LC 1137 - N-th Tribonacci Number | wider recursive dependency |
| Good to do | LC 746 - Min Cost Climbing Stairs | recursion with minimization |

## Checkpoint Questions

- What exactly does one function call mean?
- Can you identify the smallest valid input and answer it directly?
- Can you explain why the recursive calls are sufficient to solve the original problem?
- Can you tell whether a parameter is an index, a count, or a remaining target?
- Can you derive the recurrence from the problem statement instead of from memory?

## Next Up

Next subtopic: Overlapping subproblems.

That is where recursion turns into DP. Once you see repeated states in the recursion tree, memoization starts to feel inevitable instead of magical.