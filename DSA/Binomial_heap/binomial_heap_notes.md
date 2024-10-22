# Binomial Heap

A **binomial heap** is a collection of binomial trees, each of which satisfies the heap property (min-heap).

## Binomial Tree

- A binomial tree \( B_k \) is an ordered tree defined recursively:
  - The binomial tree \( B_0 \) consists of a single node.
  - The binomial tree \( B_k \) consists of two binomial trees \( B_{k-1} \) and \( B_{k-1} \) linked together.

### Properties

- Each binomial heap \( H \) obeys the min-heap property.
- For any non-negative integer \( k \), there is at most one binomial tree in \( H \) whose root has degree \( k \).
- The tree has \( 2^k \) nodes.
- The height of the tree is \( k \).
- There are exactly \( \binom{k}{i} \) nodes at level \( i \).
- The root has degree \( k \), which is greater than the children of the root, numbered from left to right as \( k-1, k-2, \dots, 0 \).

### Representation of a Binomial-Heap Node

Each node in a binomial heap contains:
- `parent`: Pointer to the parent node.
- `key`: The key of the node.
- `degree`: The degree of the node (number of children).
- `left child`: Pointer to the leftmost child.
- `sibling`: Pointer to the next sibling node.

### Example

Consider the heap structure in the image:

- **Node 13**:  
  The binary representation of 13 is `1101`, meaning it consists of \( B_3, B_2, B_0 \) binomial trees.

- **Node 9**:  
  The binary representation of 9 is `1001`, consisting of \( B_3, B_0 \).

- **Node 16**:  
  The binary representation of 16 is `10000`, consisting of \( B_4 \).

## Operations

1. **Creating a new binomial heap**: \( O(1) \)
2. **Finding the minimum key**: \( o(log n) \)
3. **Union of two binomial heaps**: \( o(log n) \)
4. **Inserting a node**: \( o(log n) \)
5. **Extracting the minimum key**: \( o(log n) \)
6. **Decreasing a key**: \( o(log n) \)
7. **Deleting a node**: \( o(log n) \)

---

# Union of Two Binomial Heaps

The union of two binomial heaps involves merging binomial trees of the same degree.

### Cases:
1. **Case 1**: If `degree[x] != degree[next[x]]`, move the pointer ahead.
2. **Case 2**: If `degree[x] == degree[next[x]]`, merge `next[x]` and `x`, then move the pointer.
3. **Case 3**: If `degree[x] == degree[next[x]]` and `key[x] < key[next[x]]`, remove `next[x]` from the root and attach it to `x`.
4. **Case 4**: If `degree[x] == degree[next[x]] + degree[sibling[next[x]]]` and `key[x] > key[next[x]]`, remove `x` from the root and attach it to `next[x]`.

# Inserting a Node into a Binomial Heap

Inserting a node into a binomial heap involves merging the new node as a single binomial tree with the current binomial heap. The process follows these steps:

1. **Create a New Binomial Heap**:
   - Create a new binomial heap \( H_1 \) containing only the new node.
   
2. **Union the New Heap with the Existing Heap**:
   - Perform a union of the current heap \( H \) with the new heap \( H_1 \). 
   - This union is done by merging binomial trees of the same degree and maintaining the min-heap property.

3. **Merging Binomial Trees**:
   - If two trees of the same degree are found, one becomes the child of the other, depending on their keys. The smaller key becomes the parent.

### Example (Referencing Image):

Consider the binomial heap structure where we insert a new node with key `18`:

1. **Initial Binomial Heap Structure**:
   The current heap \( H \) consists of trees \( B_3, B_2, B_1, B_0 \).
   - \( B_3 \): Root `15` with a subtree containing nodes `33`, `20`, and `7`.
   - \( B_2 \): Root `12` with subtree nodes `25` and `37`.
   - \( B_1 \): Root `25` with a subtree of node `29`.

2. **New Node**:
   - We want to insert a node with key `18`.

3. **Step-by-Step Process**:
   - A new binomial tree \( B_0 \) is created with root `18`.
   - Perform a union of this new tree with the existing heap.
   - **Union Process**:
     - First, link trees of equal degrees. For example, if a tree \( B_0 \) already exists in \( H \), the new tree \( B_0 \) must be merged with the existing one.
     - The trees are linked, and the smaller root becomes the parent of the larger one. Continue until no trees with the same degree remain in \( H \).

In this example, after inserting `18`, the tree structures are merged while ensuring the heap property (smallest root at the top).

### Pseudocode

```python
def insert(heap, new_node):
    # Step 1: Create a new binomial heap with the new node
    new_heap = create_new_heap(new_node)
    
    # Step 2: Union the new heap with the existing heap
    heap = union(heap, new_heap)
    
    return heap

def union(heap1, heap2):
    # Step 3: Merge trees of equal degrees
    merged_heap = merge_trees(heap1, heap2)
    
    # Maintain min-heap property during the merge
    prev_tree = None
    curr_tree = merged_heap.head
    next_tree = curr_tree.sibling
    
    while next_tree is not None:
        if curr_tree.degree != next_tree.degree or \
           (next_tree.sibling is not None and next_tree.sibling.degree == curr_tree.degree):
            prev_tree = curr_tree
            curr_tree = next_tree
        else:
            if curr_tree.key <= next_tree.key:
                curr_tree.sibling = next_tree.sibling
                link(next_tree, curr_tree)
            else:
                if prev_tree is None:
                    merged_heap.head = next_tree
                else:
                    prev_tree.sibling = next_tree
                link(curr_tree, next_tree)
                curr_tree = next_tree
        
        next_tree = curr_tree.sibling
    
    return merged_heap
```
# Extracting the Minimum Key
In a binomial heap, the minimum key is always in one of the root nodes, since it is a min-heap. The goal is to find the root with the smallest key, remove it, and reinsert its children back into the heap.

#### Steps:
1. **Find the Root with the Minimum Key**.
2. **Remove the Tree Rooted at the Minimum Key**.
3. **Reinsert the Subtrees of the Removed Root into the Heap**.

#### Algorithm:
```python
def extract_min(heap):
    # Step 1: Find the root with the minimum key
    min_node = heap.head
    min_node_prev = None
    curr = heap.head
    prev = None
    
    while curr is not None:
        if curr.key < min_node.key:
            min_node = curr
            min_node_prev = prev
        prev = curr
        curr = curr.sibling
    
    # Step 2: Remove the minimum node
    if min_node_prev is None:
        heap.head = min_node.sibling
    else:
        min_node_prev.sibling = min_node.sibling
    
    # Step 3: Reinsert the subtrees of the removed root into the heap
    child_heap = reverse_children(min_node.child)
    
    # Perform union with the remaining heap
    heap = union(heap, child_heap)
    
    return min_node, heap

def reverse_children(child):
    # This function reverses the order of children (to maintain binomial tree properties)
    prev = None
    curr = child
    while curr is not None:
        next = curr.sibling
        curr.sibling = prev
        prev = curr
        curr = next
    return prev
```
**Time Complexity**: \( O(\log n) \) (since there are \( O(\log n) \) trees and merging the heap with children takes \( O(\log n) \)).

# Decreasing a Key
To decrease the key of a node in a binomial heap, follow these steps:
1. **Find the Node** whose key needs to be decreased.
2. **Update the Key**.
3. **Bubble Up** the node to maintain the heap property.

#### Algorithm:
```python
def decrease_key(heap, node, new_key):
    if new_key > node.key:
        raise ValueError("New key must be smaller than the current key")
    
    # Step 1: Update the key
    node.key = new_key
    
    # Step 2: Bubble up the node to maintain the heap property
    current = node
    parent = current.parent
    
    while parent is not None and current.key < parent.key:
        # Swap keys between current node and parent
        current.key, parent.key = parent.key, current.key
        current = parent
        parent = current.parent
```
**Time Complexity**: \( O(\log n) \) (since a node can only bubble up along the height of a binomial tree, which is \( O(\log n) \)).

# Deleting a Node
To delete a node from a binomial heap, the following approach is taken:
1. **Decrease the Key** of the node to \( -\infty \) (or some very small number).
2. **Extract the Minimum Key** (which will now be the node to be deleted).

#### Algorithm:
```python
def delete_node(heap, node):
    # Step 1: Decrease the key of the node to -∞
    decrease_key(heap, node, float('-inf'))
    
    # Step 2: Extract the minimum key, which is now the node to be deleted
    _, heap = extract_min(heap)
    
    return heap
```
**Time Complexity**: \( O(\log n) \) for decreasing the key and \( O(\log n) \) for extracting the minimum, so the overall complexity is \( O(\log n) \).