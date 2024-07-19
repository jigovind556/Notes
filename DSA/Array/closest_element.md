# Function to find the closest element in the non-empty array

```cpp
    int closest(vector<int>& arr,int tar){
        auto it = lower_bound(arr.begin(),arr.end(),tar);
        if(it==arr.begin()) return *it;
        if(it==arr.end()) return *(--it);

        int a=*it;
        int b=*(--it);
        return (abs(a - tar)<= abs(b-tar)) ?a:b;
    }
```