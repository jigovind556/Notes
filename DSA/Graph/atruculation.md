# Atriculation point

The nodes in the graph ,whoose removal the graph breaks into two saperate component

```cpp
class Solution {
    void dfs(vector<int>adj[],vector<int>&tin,vector<int>&low,vector<int>&res,int i,int par,int& time){
        tin[i]=time;
        low[i]=time;
        time++;
        bool isa=false;
        int child=0;
        for(int it : adj[i]){
            if(it==par) continue;
            if(tin[it]==-1) {
                dfs(adj,tin,low,res,it,i,time);
                low[i]= min(low[it],low[i]);
                if(low[it]>=tin[i] && par!= -2 ) isa=true;
                child++;
            }else {
                low[i]= min(tin[it],low[i]);
            }
            
        }
        if(par==-2 && child>1) isa=true;
        if(isa) res.push_back(i);
    }
  public:
    vector<int> articulationPoints(int V, vector<int>adj[]) {
        // Code here
        
        vector<int> tin(V,-1);
        vector<int> low(V);
        vector<int> res;
        int time=0;

        for(int i=0;i<V;i++){
            if(tin[i]==-1) dfs(adj,tin,low,res,i,-2,time);
        }
        
        sort(res.begin(),res.end());
        if(res.size()==0) return {-1};
        return res;
    }
};

```