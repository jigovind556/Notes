# Longest Common Substring

You are given two strings s1 and s2. Your task is to find the length of the longest common substring among the given strings.

[Problem Link](https://www.geeksforgeeks.org/problems/longest-common-substring1452/1)

### Steps to solve
* This problem can be solved as LCs with slight modification.

* There will be only two relation
    1. if the character matches
    ```dp(i,j)= 1+dp(i-1,j-1); ```
    2. else put the length 0
    ```dp(i,j)= 0; ```

* **Note** : the answer will be the maximum element of the dp.

## Tabulation Code
```cpp
class Solution {
  public:
    int longestCommonSubstr(string s1, string s2) {
        // your code here
        int n=s1.size(),m=s2.size();
        vector<vector<int>> dp(n+1,vector<int>(m+1,0));
        
        int res=0;
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(s1[i-1]==s2[j-1]) dp[i][j]=1+dp[i-1][j-1];
                res=max(res,dp[i][j]);
            }
        }
        
        return res;
    }
};
```

## Memory Optimised
```cpp
class Solution {
  public:
    int longestCommonSubstr(string s1, string s2) {
        // your code here
        int n=s1.size(),m=s2.size();
        vector<int> prev(m+1,0);
        
        int res=0;
        for(int i=1;i<=n;i++){
            vector<int> curr(m+1,0);
            for(int j=1;j<=m;j++){
                if(s1[i-1]==s2[j-1]) curr[j]=1+prev[j-1];
                res=max(res,curr[j]);
            }
            prev=curr;
        }
        
        return res;
    }
};
```