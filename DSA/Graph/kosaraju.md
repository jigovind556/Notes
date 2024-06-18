# Kosaraju's algorithm (Strongly connected components)


**Strongly connected components(scc) :** Any component in a directed graph,such that from any node ,I can traverse all nodes (including itself) of that component.

* This algo is used to find the strongly connected components.
* It is only valid for directed graph.

## steps of algorithm
1. sort all the nodes according to finish time of dfs.
2. reverse all the edges.
3. Run the dfs again.


