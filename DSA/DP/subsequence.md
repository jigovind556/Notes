# DP on Subsequence

**Subsequence :** a sequence that can be derived from another string/sequence by deleting some or none of the elements without changing the order of the remaining elements.

### Steps to approach
1. try to express the problem in terms of index and a target.
2. explore all the possibilities of that index.(e.g. it is either part of subsequence or not the part of subsequence)

### for Tabulation
1. make a 2d dp array of size*target.
2. fill all the base cases as true.
3. now write two loops (1->n),(1->target) with the recurrence.



## Exapme of the solution of [Subset Sum Problem](https://www.geeksforgeeks.org/problems/subset-sum-problem-1611555638/1)

### Memoisation approach

```cpp
class Solution{   
    bool solve(vector<int>& arr,int i,int target,vector<vector<int>>& dp){
        if(target==0) return 1;
        if(target==arr[i]) return dp[i][target]=1;
        if(i==0) return dp[i][target]=0;
        if(dp[i][target]!=-1) return dp[i][target];
        
        //pick 
        if(arr[i]<=target && solve(arr,i-1,target-arr[i],dp)) return dp[i][target]=1;
        
        //not pick 
        
        return dp[i][target] = solve(arr,i-1,target,dp);
    }
public:
    bool isSubsetSum(vector<int>arr, int sum){
        // code here 
        vector<vector<int>> dp(arr.size(),vector<int>(sum+1,-1));
        
        return (solve(arr,arr.size()-1,sum,dp));
    }
};
```

### Tabulation approach 
```cpp
class Solution{   
public:
    bool isSubsetSum(vector<int>arr, int sum){
        // code here 
        int n=arr.size();
        vector<vector<bool>> dp(n,vector<bool>(sum+1,0));
        
        for(int i=0;i<n;i++){
            dp[i][0]=1;
        }
        dp[0][arr[0]]=1;
        
        for(int i=1;i<n;i++){
            for(int j=1;j<=sum;j++){
                bool Pick=false;
                if(arr[i]<=j) Pick = dp[i-1][j-arr[i]];
                bool notPick = dp[i-1][j];
                dp[i][j]=Pick || notPick;
            }
        }
        
        return dp[n-1][sum];
    }
};
```

### Memory optimised 
```cpp
class Solution{
public:
    bool isSubsetSum(vector<int>arr, int sum){
        // code here 
        int n=arr.size();
        vector<bool> prev(sum+1,0);
        
        prev[arr[0]]=1;
        prev[0]=1;
        
        for(int i=1;i<n;i++){
            vector<bool> curr(sum+1);
            curr[0]=1;
            for(int j=1;j<=sum;j++){
                bool Pick=false;
                if(arr[i]<=j) Pick = prev[j-arr[i]];
                bool notPick = prev[j];
                curr[j]=Pick || notPick;
            }
            prev=curr;
        }
        
        return prev[sum];
    }
};
```


/*

3,2, 5 8

9

    0   1   2   3   4   5   6   7   8
0   t   f   f   t   f   f   f   f   f
1   t   f   t   t   f   t   f   f   f
2   t   f   t   t   f   t   f   t   f
3   t   f   t   t   f   t   f   t   f
*/