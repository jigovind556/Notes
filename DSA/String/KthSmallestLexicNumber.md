# K-th smallest in lexicographical order

[Leetcode](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/description/)

Given two integers n and k, return the kth lexicographically smallest integer in the range [1, n].

### Code

```cpp
class Solution {
    int findGap(long n,long a,long b){
        long gap=0;
        while(a<=n){
            gap+= min(b,n+1)-a;
            b*=10;
            a*=10;
        }
        return gap;
    }
public:
    int findKthNumber(int n, int k) {
        int res=1;
        k--;
        while(k>0){
            int gap=findGap((long)n,(long)res,(long)res+1);
            cout<<res<<"  "<<k<<"  "<<gap<<endl;
            if(gap<=k){
                res++;
                k-=gap;
            }
            else {
                res*=10;
                k--;
            }
        }

        return res;
    }
};
```