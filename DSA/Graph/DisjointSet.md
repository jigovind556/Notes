# disjoint set
- The disjoint set data structure is used to efficiently manage a collection of disjoint sets.
- Each set is represented by a representative element, which is one of the elements in the set.
- The data structure supports two main operations: union and find.
- The union operation merges two sets into a single set.
- The find operation determines the representative element of a given element.


## code with find union by rank
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


## code with find union by size
```cpp
class DisjointSet {
    vector<int> size, parent;

    public:
    DisjointSet(int n) {
        size.resize(n + 1, 1);
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
    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);

        if (ulp_u == ulp_v)
            return;

        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u];
        } else {
            parent[ulp_v] = ulp_u;
            size[ulp_v] += size[ulp_u];
        }
    }
    int getSize(int i){
        int ulp_i=findUPar(i);
        return size[ulp_i];
    }

};

```
