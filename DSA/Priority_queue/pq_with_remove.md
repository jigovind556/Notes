# Rmove function in priority queue of c++ STL

```cpp
template<typename T, typename Container=vector<T>, typename Compare=less<typename Container::value_type>>
class custom_priority_queue : public priority_queue<T, Container, Compare> {
public:
    bool remove(const T& value) {
        auto it = find(this->c.begin(), this->c.end(), value);
        if (it == this->c.end()) {
            return false;
        }
        this->c.erase(it);
        make_heap(this->c.begin(), this->c.end(), this->comp);
        return true;
    }
};
```