# Longest Common Subsequence

Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".
A common subsequence of two strings is a subsequence that is common to both strings.

[Problem Link](https://leetcode.com/problems/longest-common-subsequence/)

## Rules to solve : 
1. Express every thing in terms of index.(ind1 , ind2)
2. Explore every possibility on that index.
3. Take the best among them.

### note :
**f(i,j)** => LCS in string a[0...i] and b[0....j]

### Recurrence relation :
* thenre are three condition 
    1. if the character matches 
    ```f(i,j)= 1+f(i-1,j-1); ```
    2. j same and i-1
    ```c2= f(i-1,j)```
    3. i same and j-1 
    ```c3= f(i,j-1)```
* Take the maximum of the two cases cases.
    ``` f(i,j) = max(c2,c3) ```


## Recursive Solution 
```cpp
class Solution {
    int solve(string &t1,string& t2,int i,int j,vector<vector<int>>& dp){
        if(i<0 || j<0) return 0;
        if(dp[i][j]!=-1) return dp[i][j];
        // pick
        if(t1[i]==t2[j]) return dp[i][j]= 1+solve(t1,t2,i-1,j-1,dp);
        // not pick
        int c1= solve(t1,t2,i-1,j,dp);
        int c2= solve(t1,t2,i,j-1,dp);

        return dp[i][j]= max(c1,c2);
    }
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<vector<int>> dp(text1.size(),vector<int>(text2.size(),-1));

        return solve(text1,text2,text1.size()-1,text2.size()-1,dp);
    }
};
```

### Tabulation code
```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int m = text1.length(), n = text2.length();
        int dp[m+1][n+1];
        for(int i=0;i<=m;i++){
            dp[i][0] = 0;
        }   
        for(int i=0;i<=n;i++){
            dp[0][i] = 0;
        }
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++){
                if(text1[i-1]==text2[j-1]){
                    dp[i][j]=1+dp[i-1][j-1];
                }
                else{
                    dp[i][j]=max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        return dp[m][n];
    }
};
```

### space optimised
```cpp  
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n=text1.size(),m=text2.size();
        vector<int> prev(m,0);

        for(int j=0;j<m;j++){
            if(j>0) prev[j]=prev[j-1];
            if(text1[0]==text2[j]) prev[j]=1;
        }
        for(int i=1;i<n;i++){
            vector<int> curr(m,0);

            if(text1[i]==text2[0]) curr[0]=1;
            else curr[0]=prev[0];

            for(int j=1;j<m;j++){
                if(text1[i]==text2[j]) curr[j]=prev[j-1]+1;
                else {
                    curr[j]=max(prev[j],curr[j-1]);
                }
            }
            prev=curr;
        }

        return prev[m-1];
    }
};
```
