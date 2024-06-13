# Bellman Ford Algorithm

- This algorithm is used to find the shortest path in the directed graph.
- For directed graph, we have to insert two edges with the same weight and opposite nodes.
- This algorithm can also detect negative cycle in the graph.
- This is also useful in the negative weight graph.


### Algorithm 
1. put all the edges in a list .(The order does not matter)
2. run a loop for n-1 time and relax all the edges.

### Why the loop run n-1 time
since in a graph of N nodes,in worst case you will take n-1 edges N-1 edges to reach from first to the last ,therefore we iterate for N-1 time.

```cpp
    vector<int> bellman_ford(int V, vector<vector<int>>& edges, int S) {        
        vector<int> dist(V,1e8); 
        dist[S]=0;
        
        for(int i=0;i<V-1;i++){
            for(auto edge : edges){
                if(dist[edge[0]] == 1e8) continue;
                int d= dist [edge[0]] + edge[2];
                if(d < dist[edge[1]]) {
                    dist[edge[1]] = d;
                }
            }
        }

        // check for the negative circle in the graph        
        for(auto edge : edges){
            if(dist[edge[0]] == 1e8) continue;
            int d= dist [edge[0]] + edge[2];
            if(d < dist[edge[1]])  return {-1};
        }
        
        return dist;
    }
```