# 0/1 Knapsack

You are given weights and values of N items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. Note that we have only one quantity of each item.

In other words, given two integer arrays val[0..N-1] and wt[0..N-1] which represent values and weights associated with N items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of val[] such that sum of the weights of this subset is smaller than or equal to W. You cannot break an item, either pick the complete item or dont pick it (0-1 property).

### Intution 
* when two values are mapped with each other but non uniformly, then we can use this concept.

### Steps
1. Express the problem in terms of index, weight.
2. explore all possibilities (pick / not pick).
3. pick maximum of all.


