---
{"dg-publish":true,"permalink":"/knowledge/cs/algorithms/algorithms/","dg-note-properties":{}}
---

## Basic Definition

> [!definition] Algorithm
> An **algorithm** is **any well-define computational procedure** that takes some value, or set of values, as **input** and produces some value, or set of values, as **output**. 

## Loop Invariant

> [!remark]
> This is a general proof technique, not bounded by any field, it will be move once I write about logical proof technique.

> [!algorithm] Using Loop Invariant in Algorithm
> Suppose that we have some property $P$ that we want to prove that after the loop, $O$ has property $P$, we can use this procedure:
> - **Initialization**: Object $O$ has property $P$ before the loop.
> - **Maintenance**: If $O$ has $P$ before an iteration of the loop, it still has $P$ before the next iteration.
> - **Termination**: When the loop terminates, we have that $O$ has $P$ and we can use it to argue that the algorithm is correct.

