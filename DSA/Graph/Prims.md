# Prim's Algorithm

This algorithm is used to find the minimum spanning tree(MST) of a graph.
* This algorithm is based on the greedy approach
* **Time complexity** : E(log E)

## Basic components
* Visited array
* priority queue (weight,node,parent)

```cpp

//Function to find sum of weights of edges of the Minimum Spanning Tree.
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        priority_queue<pair<int,int>,vector<pair<int,int>> ,greater<pair<int,int>>> pq;
        vector<bool> vis(V,0);

        // initially push the weight 0 and edge 0
        pq.push({0,0});
        int res=0;
        
        while(!pq.empty()){
            int wt= pq.top().first;
            int node = pq.top().second;
            pq.pop();
            
            if(vis[node]) continue;
            // add it to the mst
            vis[node]=1;
            res+=wt;
            
            for(auto it: adj[node]){
                int adjNode= it[0];
                int edw = it[1];
                
                if(!vis[adjNode]){
                    pq.push({edw,adjNode});
                }
            }
        }
        
        return res;
    }
```

