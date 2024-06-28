# Kosaraju's algorithm (Strongly connected components)


**Strongly connected components(scc) :** Any component in a directed graph,such that from any node ,I can traverse all nodes (including itself) of that component.

* This algo is used to find the strongly connected components.
* It is only valid for directed graph.

## steps of algorithm
1. sort all the nodes according to finish time of dfs.
2. reverse all the edges.
3. Run the dfs again.

```cpp
class DisjointSet {
    vector<int> rank, parent;

    public:
    DisjointSet(int n) {
        rank.resize(n + 1, 0);
        parent.resize(n + 1);
        for (int i = 0; i < n + 1; i++) {
            parent[i] = i;
        }
    }
    int findUPar(int i) {
        if (parent[i] == i)
            return i;
        return parent[i] = findUPar(parent[i]);
    }
    void unionByRank(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);

        if (ulp_u == ulp_v)
            return;

        if (rank[ulp_u] < rank[ulp_v]) {
            parent[ulp_u] = ulp_v;
        } else if (rank[ulp_u] > rank[ulp_v]) {
            parent[ulp_v] = ulp_u;
        } else {
            parent[ulp_v] = ulp_u;
            rank[ulp_u]++;
        }
    }

};
```
