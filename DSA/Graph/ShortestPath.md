# Shortest path to all node in a directed graph

### Algorithm

1. Do a Topological sorting on the graph.
2. make a distance array initially marked as infinity.
3. Mark the distance of source node as 0.
4. Take out nodes from the stack relax its edges.

```cpp

class Solution {
  private:
    void topoSort(int node, vector < pair < int, int >> adj[],
      int vis[], stack < int > & st) {
      //This is the function to implement Topological sort. 
      vis[node] = 1;
      for (auto it: adj[node]) {
        int v = it.first;
        if (!vis[v]) {
          topoSort(v, adj, vis, st);
        }
      }
      st.push(node);
    }
  public:
    vector < int > shortestPath(int N, int M, vector < vector < int >> & edges) {

      //We create a graph first in the form of an adjacency list.
      vector < pair < int, int >> adj[N];
      for (int i = 0; i < M; i++) {
        int u = edges[i][0];
        int v = edges[i][1];
        int wt = edges[i][2];
        adj[u].push_back({v, wt}); 
      }
      // A visited array is created with initially 
      // all the nodes marked as unvisited (0).
      int vis[N] = {
        0
      };
      //Now, we perform topo sort using DFS technique 
      //and store the result in the stack st.
      stack < int > st;
      for (int i = 0; i < N; i++) {
        if (!vis[i]) {
          topoSort(i, adj, vis, st);
        }
      }
      //Further, we declare a vector ‘dist’ in which we update the value of the nodes’
      //distance from the source vertex after relaxation of a particular node.

      vector < int > dist(N);
      for (int i = 0; i < N; i++) {
        dist[i] = 1e9;
      }

      dist[0] = 0;
      while (!st.empty()) {
        int node = st.top();
        st.pop();

        for (auto it: adj[node]) {
          int v = it.first;
          int wt = it.second;

          if (dist[node] + wt < dist[v]) {
            dist[v] = wt + dist[node];
          }
        }
      }

      for (int i = 0; i < N; i++) {
        if (dist[i] == 1e9) dist[i] = -1;
      }
      return dist;
    }
};

```


# Shortest path in undirected graph with unit weight

* use BFS to traverse the graph .
* make a distance arry and initialise it with infinity.
* put distance of source to 0.
* then update the distance of all node while traversing in BFS.


```cpp
    vector<int> shortestPath(vector<vector<int>>& edges, int N,int M, int src){
        // code here
        vector<vector<int>> adl(N);
        
        for(auto it: edges){
            adl[it[0]].push_back(it[1]);
            adl[it[1]].push_back(it[0]);
        }
        
        vector<int> dist(N,INT_MAX);
        queue<int> q;
        q.push(src);
        dist[src]=0;
        
        while(!q.empty()){
            int node=q.front();
            q.pop();
            
            for(auto it: adl[node]){
                if(dist[node] + 1 < dist[it]) {
                    dist[it] = 1 + dist[node]; 
                    q.push(it); 
                }
            }
        }
        
        for(int i=0;i<N;i++){
            if(dist[i]==INT_MAX) dist[i]=-1;
        }
        
        return dist;
    }

```