# Dijkstra's Algorithm
This algorithm is used to find the shortest path between two nodes in weighted graph.

**NOTE** : This algorithm does not work with the negative weights.

## 3 types of implementation
1. **using Priority queue** (best)
2. **using set** (better)
3. **using queue** (takes more time)

## Using priority queue
- we will use min heap of pair (node,distance).

1. make a distance array with infinite distance of all node.
2. set dist =0 for src and also push it to the min heap.

**Time Complexity** : O(E log V)
```cpp
    vector <int> dijkstra(int V, vector<vector<int>> adj[], int S)
    {
        // create a min heap 
        priority_queue<pair<int,int>,vector<pair<int,int>>, greater<pair<int,int>>> pq;
        
        // initialize a distance array
        vector<int> dist(V,1e9);
        dist[S]=0;
        pq.push({0,S});
        
        while(!pq.empty()){
            int d= pq.top().first;
            int u=pq.top().second;
            pq.pop();
            
            for( auto it : adj[u]){
                int v= it[0];
                int wt= it[1];
                if(wt+d < dist[v]){
                    dist[v]=wt+d;
                    pq.push({dist[v],v});
                }
            }
        }
        
        
        return dist;
    }
```
