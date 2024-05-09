# Kahn's algorithm 


- Topological sorting using bfs
- Uses indegree array to count the incoming edges of any node and reduces after visiting its parent



```cpp
    vector<int> topoSort(int V, vector<int> adj[]) 
        {
            // code here
            vector<int> indegree(V,0);
            for(int i=0;i<V;i++){
                for(int j=0;j<adj[i].size();j++){
                    indegree[adj[i][j]]++;
                }
            }
            
            queue<int> q;
            vector<int> topo;
            
            for(int i=0;i<V;i++) if(indegree[i]==0) q.push(i);
            
            while(!q.empty()){
                int curr=q.front();
                q.pop();
                topo.push_back(curr);
                
                for(int i:adj[curr]){
                    indegree[i]--;
                    if(indegree[i]==0) q.push(i);
                }   
            }
            
            return topo;
        }
```


### use cases

- cycle detection using the BFS algorithm .
    * if the topological sort produced is not of the size n , then the graph has a cycle.

