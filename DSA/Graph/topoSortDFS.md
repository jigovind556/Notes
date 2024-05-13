# Topological sort using DFS

```cpp
    void dfs(vector<vector<pair<int,int>>>& adl,vector<bool>& vis,vector<int>& topo,int i){
        vis[i]=true;
        
        for(pair<int,int> j:adl[i]){
            if(!vis[j.first]){
                dfs(adl,vis,topo,j.first);
            }
        }
        topo.push_back(i);
    }
    
    vector<int> topoSort(vector<vector<pair<int,int>>> & adl){
        vector<bool> vis(adl.size(),false);
        vector<int> topo;
        
        for(int i =0;i<adl.size();i++){
            if(!vis[i]){
                dfs(adl,vis,topo,i);
            }
        }
        
        return topo;
    }

```