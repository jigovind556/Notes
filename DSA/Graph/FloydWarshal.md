# Floyd Warshal Algorithm

- This algorithm is used to find shortest path from multiple source.
- The algorithm is not much intutive as the other one.
- It is more brute force, where all combination of paths have been tried to get the shortest path.
- Traverse all the edge and calculate distance between all the edges.

**Time Complexity** : n^3 

```cpp
    void shortest_distance(vector<vector<int>>&matrix){
	    
	    int n= matrix.size();
	    // assign infinity to each -1 (unreachable node)
	    for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==-1) {
                    matrix[i][j] = 1e8;
                }
            }
        }
	    
        // floyd warshal algorithm .
	    for(int k=0;k<n;k++){
	        for(int i=0;i<n;i++){
	            for(int j=0;j<n;j++){
                    int d= matrix[i][k] + matrix[k][j];
                    matrix[i][j]= min(d,matrix[i][j]);
	            }
	        }
	    }
	    
        // change infinity to -1 
	    for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==1e8) {
                    matrix[i][j] = -1;
                }
            }
        }
            
	}
```

## How to detect a negative cycle ? 

If the any node is non zero ``` mat[i][i] != 0 ``` then it has a negative cycle.