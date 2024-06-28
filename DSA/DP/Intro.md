# Dynamic Programming 

## Memoisation 
* If i tend to store the value of subProblems in a table or map .
* It is a **Top Down** approach.

* **Time Complexity :** O(N)
* **Space Complexity :** O(N)

## Tabulation

* It is a **Bottom Up** Approach 
* **Time Complexity :** O(N)
* **Space Complexity :** O(N)

### Steps
1. initialise the dp array.
2. fill the base case in dp array.
3. complete the dp array starting from the base case.

**NOTE :** Tabulattion is better solution as we save the recursion stack.

## Example code for fibonacci number

### memoisation 
```cpp
#include <bits/stdc++.h>

using namespace std;

int f(int n, vector<int>& dp){
    if(n<=1) return n;
    
    if(dp[n]!= -1) return dp[n];
    return dp[n]= f(n-1,dp) + f(n-2,dp);
}


int main() {

  int n=5;
  vector<int> dp(n+1,-1);
  cout<<f(n,dp);
  return 0;
}
```

### Tabulation

```cpp
#include <bits/stdc++.h>

using namespace std;


int main() {

  int n=5;
  vector<int> dp(n+1,-1);
  
  dp[0]= 0;
  dp[1]= 1;
  
  for(int i=2; i<=n; i++){
      dp[i] = dp[i-1]+ dp[i-2];
  }
  cout<<dp[n];
  return 0;
}
```

### Space optimised code
* **Time Complexity:** O(N)
* **Space Complexity:** O(1)
```cpp
#include <bits/stdc++.h>

using namespace std;


int main() {

  int n=5;
  
  int prev2 = 0;
  int prev = 1;
  
  for(int i=2; i<=n; i++){
      int cur_i = prev2+ prev;
      prev2 = prev;
      prev= cur_i;
  }
  cout<<prev;
  return 0;
}

```
