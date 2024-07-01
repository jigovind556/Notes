# Tree

* number of node : n
* number of edges : n-1


## find root in undirected graph

```cpp
    int find_root(vector<vector<int>>& adj){
        int n=adj.size();
        vector<int> degree(n,0);
        for(int i=0;i<n;i++){
            degree[i]=adj[i].size();
        }
        
        queue<int> q;
        for(int i=0;i<n;i++){
            if(degree[i]==1) q.push(i);
        }
        int root=0;
        while(!q.empty()){
            int u=q.front();
            q.pop();
            root=u;
            for(auto v: adj[u]){
                degree[v]--;
                if(degree[v]==1) q.push(v);
            }
        }
        return root;
    }
```


## find the diameter of the tree
```cpp
    int find_root(vector<vector<int>>& adj){
        int n=adj.size();
        vector<int> degree(n,0);
        for(int i=0;i<n;i++){
            degree[i]=adj[i].size();
        }
        
        queue<int> q;
        for(int i=0;i<n;i++){
            if(degree[i]==1) q.push(i);
        }
        int root=0;
        while(!q.empty()){
            int u=q.front();
            q.pop();
            root=u;
            for(auto v: adj[u]){
                degree[v]--;
                if(degree[v]==1) q.push(v);
            }
        }
        return root;
    }
    int dfs_h(vector<vector<int>>& adj,int i,vector<bool>& vis){
        vis[i]=true;    
        int res=0;
        for( auto it : adj[i]){
            if(!vis[it]){
                res = max(res,dfs_h(adj,it,vis));
            }
        }
        return 1+res;
    }
    vector<int> find_dia(vector<vector<int>>& adj){
        if(adj.size()==1) return {0,0,0};
        int root = find_root(adj);
        priority_queue<int> pq; 
        vector<bool> vis(adj.size(),false);
        vis[root]=true;
        for(auto it: adj[root]){
            int temp=dfs_h(adj,it,vis);
            cout<<it<<"  "<< temp<<endl;
            pq.push(temp);
        }
        if(pq.size()<2){
            int h=pq.top();
            return {root,h,h};//root, max height, diameter
        }
        
        int h1=pq.top();
        pq.pop();
        int h2=pq.top();
        
        cout<< root<<"  " <<h1 << "  " <<h1+h2<<endl;
        return {root,h1,h1+h2};//root, max height, diameter
        
    }
```