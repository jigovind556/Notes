# Kruskal's Algorithm

This algorithm is used to find the minimum spanning tree (MST) from a graph.
* It uses [Disjoint set](./DisjointSet.md) data structure to find the MST.

## Steps of the Algorithm

1. Sort all the edges in the increasing order of weight.
2. Traverse all the edge.
3. for edge (u,v,wt) ,add it to the MST if it is not part of it.


```cpp
int spanningTree(int V, vector<vector<int>> adj[])
    {
        // store all the edges in a array (wt, u,v)
        vector<vector<int>> edges;
        for(int i=0;i<V;i++){
            for(auto it : adj[i]){
                edges.push_back({it[1],i,it[0]});
            }
        }
        //sort edges
        sort(edges.begin(),edges.end());
        
        DisjointSet ds(V);
        
        int res=0;
        
        for(auto it: edges){
            int x= ds.findUPar(it[1]);
            int y= ds.findUPar(it[2]);
            
            if(x!=y){
                // add it to MST
                res+=it[0];
                ds.unionByRank(it[1],it[2]);
            }
        }
        return res;
        
    }

```