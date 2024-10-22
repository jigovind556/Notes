# Binomial Heap

A **binomial heap** is a collection of binomial trees, each of which satisfies the heap property (min-heap).

## Binomial Tree

- A binomial tree \( B_k \) is an ordered tree defined recursively:
  - The binomial tree \( B_0 \) consists of a single node.
  - The binomial tree \( B_k \) consists of two binomial trees \( B_{k-1} \) and \( B_{k-1} \) linked together.

### Properties

- The tree has \( 2^k \) nodes.
- The height of the tree is \( k \).
- There are exactly \( \binom{k}{i} \) nodes at level \( i \).
- The root has degree \( k \), which is greater than the children of the root, numbered from left to right as \( k-1, k-2, \dots, 0 \).

## Operations

1. **Creating a new binomial heap**: \( O(1) \)
2. **Finding the minimum key**: \( O(\log n) \)
3. **Union of two binomial heaps**: \( O(\log n) \)
4. **Inserting a node**: \( O(\log n) \)
5. **Extracting the minimum key**: \( O(\log n) \)
6. **Decreasing a key**: \( O(\log n) \)
7. **Deleting a node**: \( O(\log n) \)

---

# Union of Two Binomial Heaps

The union of two binomial heaps involves merging binomial trees of the same degree.

### Cases:
1. **Case 1**: If `degree[x] != degree[next[x]]`, move the pointer ahead.
2. **Case 2**: If `degree[x] == degree[next[x]]`, merge `next[x]` and `x`, then move the pointer.
3. **Case 3**: If `degree[x] == degree[next[x]]` and `key[x] < key[next[x]]`, remove `next[x]` from the root and attach it to `x`.
4. **Case 4**: If `degree[x] == degree[next[x]] + degree[sibling[next[x]]]` and `key[x] > key[next[x]]`, remove `x` from the root and attach it to `next[x]`.
