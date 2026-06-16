Here’s a practical LinkedList pattern checklist you can use in interviews and coding problems:

- ✅ Dummy node pattern  
- ✅ Previous pointer pattern  
- ✅ Fast and slow pointer pattern  
- ✅ Two-pointer gap pattern  
- ✅ Reverse pointers pattern  
- ✅ Head/tail tracking pattern  
- ✅ Recursion pattern  
- ✅ Merge/build-new-list pattern  
- ✅ Cycle detection pattern  
- ✅ Common traps and mental rules  

---

# Standard LinkedList Tricks and Patterns

## 1. Dummy Node Pattern

### When to use it

Use a dummy node when the answer list may have a changing head.

This is one of the most important LinkedList tricks.

### Why?

In LinkedList problems, handling the head separately is annoying because deleting, inserting, or merging at the beginning needs special logic.

A dummy node gives you a fake node before the real head, so every operation becomes the same.

```java
Node dummy = new Node(-1);
Node curr = dummy;

// attach nodes to curr.next
curr.next = someNode;
curr = curr.next;

return dummy.next;
```

---

## Problems that use dummy node

### Common problem types

| Problem | Why dummy helps |
|---|---|
| Merge two sorted lists | Result head is unknown |
| Remove elements from list | Head itself may be removed |
| Partition list | Need to build new lists |
| Add two numbers | Result list is built digit by digit |
| Remove duplicates | May need to skip nodes |
| Reverse nodes in k-group | Head may change after reversal |
| Swap pairs | First pair may change head |

---

## Example 1: Merge Two Sorted Lists

Without dummy, you have to handle the first node separately.

With dummy:

```java
Node dummy = new Node(-1);
Node tail = dummy;

while (l1 != null && l2 != null) {
    if (l1.data <= l2.data) {
        tail.next = l1;
        l1 = l1.next;
    } else {
        tail.next = l2;
        l2 = l2.next;
    }
    tail = tail.next;
}

if (l1 != null) {
    tail.next = l1;
} else {
    tail.next = l2;
}

return dummy.next;
```

### Key idea

`dummy` stays fixed.  
`tail` moves and builds the result.

---

## Example 2: Remove All Nodes With Given Value

```java
Node dummy = new Node(-1);
dummy.next = head;

Node curr = dummy;

while (curr.next != null) {
    if (curr.next.data == val) {
        curr.next = curr.next.next;
    } else {
        curr = curr.next;
    }
}

return dummy.next;
```

### Why dummy?

If the original `head` itself needs to be deleted, dummy handles it cleanly.

Example:

```text
head = 7 -> 7 -> 1 -> 2
val = 7
```

Without dummy, deleting the head needs special logic.

With dummy:

```text
dummy -> 7 -> 7 -> 1 -> 2
```

You always delete using `curr.next`.

---

# 2. Previous Pointer Pattern

## When to use it

Use a `prev` pointer when you need to modify or delete the current node.

In a singly linked list, you cannot go backward. So if you want to remove `curr`, you need the node before it.

```java
prev.next = curr.next;
```

---

## Problems that use prev pointer

| Problem | Why prev is needed |
|---|---|
| Delete a node by value | Need to bypass current node |
| Remove duplicates | Need to skip duplicate nodes |
| Reverse list | Need previous node for pointer reversal |
| Detect and remove cycle | Need node before cycle start |
| Partition list | Need to detach nodes |
| Remove nth node from end | Need node before target |
| Reverse sublist | Need node before reversed section |

---

## Example: Delete a Node

```java
Node prev = null;
Node curr = head;

while (curr != null) {
    if (curr.data == target) {
        if (prev == null) {
            head = curr.next;
        } else {
            prev.next = curr.next;
        }
        break;
    }

    prev = curr;
    curr = curr.next;
}
```

### But better with dummy

```java
Node dummy = new Node(-1);
dummy.next = head;

Node prev = dummy;
Node curr = head;

while (curr != null) {
    if (curr.data == target) {
        prev.next = curr.next;
        break;
    }

    prev = curr;
    curr = curr.next;
}

return dummy.next;
```

### Rule

If deleting nodes, often use:

```java
prev.next = curr.next;
```

If deleting may include the head, add dummy.

---

# 3. Fast and Slow Pointer Pattern

## When to use it

Use fast and slow pointers when you need to detect structure based on distance or speed.

```java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
```

---

## Problems that use fast/slow

| Problem | Pattern |
|---|---|
| Find middle of linked list | Slow reaches middle |
| Detect cycle | Fast catches slow |
| Find cycle start | Reset one pointer to head |
| Check palindrome | Find middle, reverse second half |
| Reorder list | Find middle, reverse second half, merge |
| Split list into halves | Slow gives midpoint |

---

## Example: Find Middle Node

```java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}

return slow;
```

### For odd length

```text
1 -> 2 -> 3 -> 4 -> 5
          ^
        middle
```

### For even length

```text
1 -> 2 -> 3 -> 4
          ^
      second middle
```

This returns the second middle.

---

# 4. Two Pointer Gap Pattern

## When to use it

Use this when you need the nth node from the end.

Move one pointer ahead by `n`, then move both together.

```java
Node first = head;
Node second = head;

for (int i = 0; i < n; i++) {
    first = first.next;
}

while (first != null) {
    first = first.next;
    second = second.next;
}
```

Now `second` is the nth node from the end.

---

## Problems that use this

| Problem | Why |
|---|---|
| Remove nth node from end | Need node before nth from end |
| Find kth from end | Gap of k |
| Rotate list | Need length or kth from end |
| Split list at position from end | Gap pointer helps |

---

## Example: Remove Nth Node From End

```java
Node dummy = new Node(-1);
dummy.next = head;

Node first = dummy;
Node second = dummy;

for (int i = 0; i <= n; i++) {
    first = first.next;
}

while (first != null) {
    first = first.next;
    second = second.next;
}

second.next = second.next.next;

return dummy.next;
```

### Why `i <= n`?

Because `second` should stop at the node before the node we delete.

Example:

```text
1 -> 2 -> 3 -> 4 -> 5
n = 2
delete 4
```

We want `second` at `3`.

---

# 5. Reverse Pointer Pattern

## When to use it

Use this when changing the direction of links.

Classic three-pointer method:

```java
Node prev = null;
Node curr = head;

while (curr != null) {
    Node next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
}

return prev;
```

---

## Problems that use reversal

| Problem | Why |
|---|---|
| Reverse linked list | Direct use |
| Reverse sublist | Reverse part of list |
| Reverse nodes in k-group | Reverse chunks |
| Check palindrome | Reverse second half |
| Reorder list | Reverse second half |
| Add numbers stored forward | Reverse before addition |

---

## Mental model

Before changing `curr.next`, save the next node.

```java
Node next = curr.next;
```

Because after this:

```java
curr.next = prev;
```

you lose access to the original next node unless you saved it.

---

# 6. Head and Tail Tracking Pattern

## When to use it

Use this when you are building or maintaining a list.

Usually:

```java
Node head = null;
Node tail = null;
```

or better:

```java
Node dummy = new Node(-1);
Node tail = dummy;
```

---

## Problems that use head/tail tracking

| Problem | Use |
|---|---|
| Build linked list from array | Track tail |
| Merge lists | Tail attaches smaller node |
| Partition list | Two dummy heads and tails |
| Add two numbers | Tail appends digits |
| Flatten linked list | Tail appends child nodes |

---

## Example: Build List

```java
Node dummy = new Node(-1);
Node tail = dummy;

for (int value : values) {
    tail.next = new Node(value);
    tail = tail.next;
}

return dummy.next;
```

---

# 7. Two Dummy Lists Pattern

## When to use it

Use this when splitting nodes into two categories.

Example:

- less than `x`
- greater than or equal to `x`

```java
Node smallDummy = new Node(-1);
Node largeDummy = new Node(-1);

Node small = smallDummy;
Node large = largeDummy;
```

---

## Problems that use this

| Problem | Categories |
|---|---|
| Partition list | Less than x / greater than equal x |
| Odd-even linked list | Odd index / even index |
| Separate positive and negative | Negative / non-negative |
| Stable filtering | Keep / discard |
| Rearrange by condition | Category A / Category B |

---

## Example: Partition List

```java
Node beforeDummy = new Node(-1);
Node afterDummy = new Node(-1);

Node before = beforeDummy;
Node after = afterDummy;

while (head != null) {
    if (head.data < x) {
        before.next = head;
        before = before.next;
    } else {
        after.next = head;
        after = after.next;
    }

    head = head.next;
}

after.next = null;
before.next = afterDummy.next;

return beforeDummy.next;
```

### Important trap

Always terminate the second list:

```java
after.next = null;
```

Otherwise, old links may create unexpected cycles or wrong ordering.

---

# 8. Cycle Detection Pattern

## When to use it

Use Floyd's cycle detection when a list may contain a loop.

```java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow == fast) {
        return true;
    }
}

return false;
```

---

## Problems that use this

| Problem | Use |
|---|---|
| Detect cycle | Fast meets slow |
| Find cycle start | Reset one pointer |
| Find duplicate number | Treat array as linked list |
| Happy number | Cycle in number sequence |
| Circular linked list | Check loop |

---

## Find cycle start

```java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow == fast) {
        Node entry = head;

        while (entry != slow) {
            entry = entry.next;
            slow = slow.next;
        }

        return entry;
    }
}

return null;
```

---

# 9. Reverse Second Half Pattern

## When to use it

Use this when comparing or rearranging two halves of a list.

---

## Problems that use this

| Problem | Why |
|---|---|
| Palindrome linked list | Compare first half and reversed second half |
| Reorder list | Merge first half with reversed second half |
| Fold linked list | Pair front and back nodes |

---

## Example: Palindrome List

Steps:

1. Find middle using slow/fast.
2. Reverse second half.
3. Compare first half and second half.

```java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}

Node second = reverse(slow);
Node first = head;

while (second != null) {
    if (first.data != second.data) {
        return false;
    }

    first = first.next;
    second = second.next;
}

return true;
```

---

# 10. Reverse Sublist Pattern

## When to use it

Use this when reversing nodes between positions.

Example:

```text
1 -> 2 -> 3 -> 4 -> 5
reverse from 2 to 4
1 -> 4 -> 3 -> 2 -> 5
```

---

## Problems that use this

| Problem | Pattern |
|---|---|
| Reverse linked list II | Reverse between left and right |
| Reverse k-group | Repeated sublist reversal |
| Swap nodes in pairs | k = 2 reversal |
| Rotate in chunks | Reverse sections |

---

## Standard trick

Use dummy because reversing may start at head.

```java
Node dummy = new Node(-1);
dummy.next = head;

Node before = dummy;

for (int i = 1; i < left; i++) {
    before = before.next;
}

Node curr = before.next;

for (int i = 0; i < right - left; i++) {
    Node move = curr.next;
    curr.next = move.next;
    move.next = before.next;
    before.next = move;
}

return dummy.next;
```

### Mental model

You repeatedly take the node after `curr` and move it to the front of the reversed section.

---

# 11. Recursion Pattern

## When to use it

Use recursion when the problem naturally depends on the rest of the list.

---

## Problems that use recursion

| Problem | Why recursion helps |
|---|---|
| Reverse linked list recursively | Reverse rest, attach current |
| Merge two lists recursively | Choose smaller head |
| Remove nodes recursively | Process tail first |
| Add two numbers forward order | Recursion handles carry from end |
| Palindrome check | Compare front and back via recursion |

---

## Example: Recursive Reverse

```java
Node reverse(Node head) {
    if (head == null || head.next == null) {
        return head;
    }

    Node newHead = reverse(head.next);

    head.next.next = head;
    head.next = null;

    return newHead;
}
```

### Be careful

Recursion uses call stack space.

For long linked lists, iterative solution is often safer.

---

# 12. Common LinkedList Decision Table

## If the problem says...

| Problem statement clue | Likely pattern |
|---|---|
| Remove/delete nodes | Dummy + prev |
| Build a result list | Dummy + tail |
| Merge sorted lists | Dummy + tail |
| Find middle | Slow + fast |
| Detect cycle | Slow + fast |
| Nth from end | Two-pointer gap |
| Reverse list | Prev/curr/next |
| Reverse between positions | Dummy + sublist reversal |
| Reverse every k nodes | Dummy + group reversal |
| Compare front and back | Reverse second half |
| Reorder list | Middle + reverse + merge |
| Split into categories | Two dummy lists |
| Head may change | Dummy node |
| Need node before target | Prev pointer |
| Need stable order | Dummy lists with tail |
| Need O(1) space | Pointer manipulation, avoid array |

---

# 13. When Exactly to Create a Dummy Node?

Create a dummy node when:

## 1. You are returning a newly built list

Example:

```java
dummy -> result nodes
return dummy.next;
```

Used in:

- merge two lists
- add two numbers
- clone list
- build filtered list

---

## 2. The head may be removed

Example:

```text
Remove value 5:
5 -> 5 -> 1 -> 2
```

Head changes from `5` to `1`.

Use:

```java
dummy.next = head;
```

---

## 3. The head may be changed by reversal

Example:

```text
1 -> 2 -> 3
reverse first two nodes
2 -> 1 -> 3
```

Use dummy to simplify reconnecting.

---

## 4. You need to attach nodes one by one

Example:

```java
tail.next = node;
tail = tail.next;
```

---

## 5. You need to avoid special-case logic

If your code has many conditions like:

```java
if (head == null)
if (prev == null)
if (newHead == null)
```

A dummy node may simplify it.

---

# 14. When to Use Prev Node?

Use `prev` when:

## 1. You want to delete `curr`

```java
prev.next = curr.next;
```

---

## 2. You want to insert before/after `curr`

```java
prev.next = newNode;
newNode.next = curr;
```

---

## 3. You are reversing links

```java
curr.next = prev;
```

---

## 4. You need the node before a target

Example:

- remove nth from end
- reverse between `left` and `right`
- remove duplicates
- unlink cycle

---

## 5. You need to reconnect after modifying a section

For example, reversing a sublist:

```text
before -> reversed section -> after
```

You need `before` to reconnect the list.

---

# 15. Standard Pointer Naming

Use consistent names. It makes LinkedList problems easier.

| Name | Meaning |
|---|---|
| `head` | First real node |
| `dummy` | Fake node before head/result |
| `curr` | Current node being processed |
| `prev` | Node before current |
| `next` | Saved next node |
| `slow` | Moves one step |
| `fast` | Moves two steps |
| `tail` | Last node of built list |
| `first` | Leading pointer |
| `second` | Trailing pointer |
| `before` | Node before a section |
| `after` | Node after a section |

---

# 16. Most Important LinkedList Trap

## Trap 1: Losing access to the rest of the list

Bad:

```java
curr.next = prev;
curr = curr.next;
```

After `curr.next = prev`, `curr.next` no longer points forward.

Correct:

```java
Node next = curr.next;
curr.next = prev;
prev = curr;
curr = next;
```

---

## Trap 2: Forgetting to return `dummy.next`

Bad:

```java
return dummy;
```

Correct:

```java
return dummy.next;
```

---

## Trap 3: Forgetting to move `tail`

Bad:

```java
tail.next = new Node(5);
```

Correct:

```java
tail.next = new Node(5);
tail = tail.next;
```

---

## Trap 4: Forgetting to cut old links

Common in partition/rearrange problems.

```java
tail.next = null;
```

This prevents accidental cycles or leftover nodes.

---

## Trap 5: Wrong loop condition for fast/slow

Safe condition:

```java
while (fast != null && fast.next != null)
```

Not safe:

```java
while (fast.next != null)
```

because `fast` itself may become `null`.

---

# 17. Quick Pattern Examples

## Delete pattern

```java
Node dummy = new Node(-1);
dummy.next = head;

Node prev = dummy;
Node curr = head;

while (curr != null) {
    if (shouldDelete(curr)) {
        prev.next = curr.next;
    } else {
        prev = curr;
    }

    curr = curr.next;
}

return dummy.next;
```

---

## Build result pattern

```java
Node dummy = new Node(-1);
Node tail = dummy;

while (condition) {
    tail.next = new Node(value);
    tail = tail.next;
}

return dummy.next;
```

---

## Reverse pattern

```java
Node prev = null;
Node curr = head;

while (curr != null) {
    Node next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
}

return prev;
```

---

## Find middle pattern

```java
Node slow = head;
Node fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}

return slow;
```

---

## Nth from end pattern

```java
Node first = head;
Node second = head;

for (int i = 0; i < n; i++) {
    first = first.next;
}

while (first != null) {
    first = first.next;
    second = second.next;
}

return second;
```

---

# 18. Interview Memory Trick

Remember this:

```text
Dummy = head may change or result is being built
Prev = need node before current
Fast/Slow = middle or cycle
Gap = nth from end
Reverse = save next first
Tail = attaching nodes
Two dummies = split into two groups
```

---

# 19. Best Problem Practice Order

If you want to master LinkedList, practice in this order:

1. Reverse Linked List
2. Merge Two Sorted Lists
3. Remove Linked List Elements
4. Middle of Linked List
5. Linked List Cycle
6. Remove Nth Node From End
7. Palindrome Linked List
8. Add Two Numbers
9. Odd Even Linked List
10. Partition List
11. Reverse Linked List II
12. Swap Nodes in Pairs
13. Reverse Nodes in k-Group
14. Reorder List
15. Copy List With Random Pointer

---

# 20. Final Cheat Sheet

| Pattern | Use When | Main Pointers |
|---|---|---|
| Dummy node | Head may change/result list built | `dummy`, `tail` |
| Prev pointer | Delete/insert/reconnect | `prev`, `curr` |
| Fast slow | Middle/cycle | `slow`, `fast` |
| Gap pointer | Nth from end | `first`, `second` |
| Reverse | Change link direction | `prev`, `curr`, `next` |
| Two dummies | Split list by condition | `before`, `after` |
| Tail pointer | Append nodes | `tail` |
| Recursion | Tail-first logic | call stack |

Best rule:

```text
If you are confused in a LinkedList problem, ask:
1. Can the head change? Use dummy.
2. Am I deleting/inserting? Track prev.
3. Do I need middle/cycle? Use fast/slow.
4. Do I need kth from end? Use gap.
5. Am I reversing? Save next first.
6. Am I building a list? Use dummy + tail.
```

