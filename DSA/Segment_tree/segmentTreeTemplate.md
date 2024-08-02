# Segment Tree

```cpp
#include <iostream>
#include <vector>
#include <functional>
#include <limits>
#include <climits>

using namespace std;

template<typename T> 
class segment_tree {
    vector<T> arr; // Original array
    vector<T> segTree; // Segment tree heap
    function<T(T, T)> operation; // Operation to be performed
    T Identity; // Identity element for the operation

    // Build the segment tree
    // create the segmement tree array as heap array
    void createSegTree(int ail, int air, int sti) {
        if (ail == air) {
            segTree[sti] = arr[ail];
            return;
        }
        int mid = (ail + air) / 2;
        createSegTree(ail, mid, sti * 2 + 1);
        createSegTree(mid + 1, air, sti * 2 + 2);
        segTree[sti] = operation(segTree[sti * 2 + 1], segTree[sti * 2 + 2]);
    }

    // Update a single element in the segment tree
    void updateSegTree(int ail, int air, int sti, int index, T val) {
        if (ail > index || air < index) return;
        if (ail == air && ail == index) {
            arr[index] = val;
            segTree[sti] = arr[index];
            return;
        }
        int mid = (ail + air) / 2;
        updateSegTree(ail, mid, sti * 2 + 1, index, val);
        updateSegTree(mid + 1, air, sti * 2 + 2, index, val);
        segTree[sti] = operation(segTree[sti * 2 + 1], segTree[sti * 2 + 2]);
    }

    // Query the range [left, right]
    T query(int ail, int air, int sti, int left, int right) {
        if (right < ail || left > air) return Identity;
        if (left <= ail && right >= air) return segTree[sti];

        int mid = (ail + air) / 2;
        T l = query(ail, mid, sti * 2 + 1, left, right);
        T r = query(mid + 1, air, sti * 2 + 2, left, right);

        return operation(l, r);
    }

  public:
    // Constructor with default operation (sum)
    segment_tree(vector<T>& nums) {
        arr = nums;
        segTree.resize(4 * nums.size());
        operation = [](T a, T b) -> T { return a + b; };  // Default operation
        Identity = 0;  // Identity for sum  
        createSegTree(0, nums.size() - 1, 0);
    }

    /*
    Constructor with custom operation and identity element. 
    
    nums: Original array
    op: Operation to be performed
    identity: Identity element for the operation
    Example: For maximum operation, identity = INT_MIN
    */
    segment_tree(vector<T>& nums, function<T(T, T)> op , T identity) {
        arr = nums;
        segTree.resize(4 * nums.size());
        operation = op;
        Identity = identity;
        createSegTree(0, nums.size() - 1, 0);
    }

    // Update element at index
    void update(int index, T val) {
        updateSegTree(0, arr.size() - 1, 0, index, val);
    }

    // Query the range [left, right]
    T queryRange(int left, int right) {
        return query(0, arr.size() - 1, 0, left, right);
    }
};

int main() {
    vector<int> nums = {1, 3, 0, 13, 9, 11};
    
    // Initialize the segment tree with the maximum operation
    segment_tree<int> st(nums, [](int a, int b) -> int { return max(a,b); } ,INT_MIN);
    // segment_tree<int> st(nums);

    // Query the maximum of the entire range
    cout << "Maximum of range [1, 2]: " << st.queryRange(1, 2) << endl;  // Output: 11

    // Update index 2 to value 10
    st.update(2, 15);

    // Query again after the update
    cout << "Maximum of range [0, 5] after update: " << st.queryRange(0, 5) << endl;  // Output: 11

    return 0;
}

```