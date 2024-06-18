# Bridge edge in a graph / Critical Connections in a Network

There are n servers numbered from 0 to n - 1 connected by undirected server-to-server connections forming a network where connections[i] = [ai, bi] represents a connection between servers ai and bi. Any server can reach other servers directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some servers unable to reach some other server.

Return all critical connections in the network in any order.

```cpp
class Solution {
    void dfs(vector<vector<int>> &adj,vector<int>&tin,vector<int>&low,vector<vector<int>>&res,int i,int par,int& time){
        tin[i]=time;
        low[i]=time;
        time++;
        for(int it : adj[i]){
            if(it==par) continue;
            if(tin[it]==-1) {
                dfs(adj,tin,low,res,it,i,time);
                if(low[it]>tin[i]) res.push_back({i,it});
            }
            low[i]= min(low[it],low[i]);
        }
    }
public:
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        vector<vector<int>> adj(n);
        for(auto it : connections){
            adj[it[0]].push_back(it[1]);
            adj[it[1]].push_back(it[0]);
        }

        vector<int> tin(n,-1);
        vector<int> low(n);
        vector<vector<int>> res;
        int time=0;

        for(int i=0;i<n;i++){
            if(tin[i]==-1) dfs(adj,tin,low,res,i,-2,time);
        }

        return res;
    }
};
```