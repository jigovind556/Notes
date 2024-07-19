# Meet in the middle algorithm 

It is used find  the [Closest Subsequence Sum](https://leetcode.com/problems/closest-subsequence-sum/description/) problem.

### steps :
1. Divide the array into two equal halfs.(if number of eleent is odd then add a element 0 at last).
2. find all possible subsequence sum of both the array and store it in two arrays.
3. sort one of the produced array.
4. find the solution.


### Code :

```cpp
class Solution {
    void solveSum(vector<int>& nums,int i,int n,int curr,vector<int>& st){
        if(i>=n){
            st.push_back(curr);
            return;
        }
        solveSum(nums,i+1,n,curr+nums[i],st);
        solveSum(nums,i+1,n,curr,st);
    }
    int closest(vector<int>& arr,int tar){
        auto it = lower_bound(arr.begin(),arr.end(),tar);
        if(it==arr.begin()) return *it;
        if(it==arr.end()) return *(--it);

        int a=*it;
        int b=*(--it);
        return (abs(a - tar)<= abs(b-tar)) ?a:b;
    }
public:
    int minAbsDifference(vector<int>& nums, int goal) {
        vector<int> stl,str;
        int n=nums.size();
        if(n&1) nums.push_back(0);
        solveSum(nums,0,(n+1)/2,0,stl);
        solveSum(nums,(n+1)/2,n,0,str);

        sort(str.begin(),str.end());
        int res=INT_MAX;

        for(int it1 : stl){
            int it2= closest(str,goal-it1);

            int sum = it1+it2;
            res= min(abs(sum-goal),res);
        }

        return res;
    }
};
```