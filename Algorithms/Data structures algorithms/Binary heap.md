```ad-note
title: Complexidade
collapse: true

- Top: $O(1)$
- Insert/remove: $O(\log n)$
```

```cpp
class BinaryHeap {
public:
    BinaryHeap(bool is_min_heap = false) : tree(1) {
        this->is_min_heap = is_min_heap;
    }

    void push(int val) {
        this->tree.push_back(val);

        this->fix_push(this->tree.size() - 1);
    }

    void pop() {
        if (this->tree.size() == 1) {
            throw std::runtime_error("Binary heap size == 0");
        }

        swap(this->tree[1], this->tree.back());

        this->tree.pop_back();

        fix_pop(1);
    }

    int top() {
        if (this->tree.size() == 1) {
            throw std::runtime_error("Binary heap size == 0");
        }

        return this->tree[1];
    }
    
    bool empty() {
        return tree.size() == 1;
    }
    
private:
    vector<int> tree;
    bool is_min_heap;

    int get_parent(int node) {
        return node / 2;
    }

    int get_left(int node) {
        return node * 2;
    }

    int get_right(int node) {
        return node * 2 + 1;
    }

    void fix_push(int node) {
        if (node == 1) {
            return;
        }

        if ((!this->is_min_heap && tree[this->get_parent(node)] > tree[node])
            || (this->is_min_heap && tree[this->get_parent(node)] < tree[node])
        ) {
            return;
        }

        swap(tree[this->get_parent(node)], tree[node]);

        this->fix_push(this->get_parent(node));
    }

    void fix_pop(int node) {
        if (this->get_left(node) >= tree.size()) {
            return;
        }

        int child_node {this->get_left(node)};

        if (this->get_right(node) < tree.size() 
            && (!this->is_min_heap && tree[this->get_left(node)] <= tree[this->get_right(node)]
            || this->is_min_heap && tree[this->get_left(node)] >= tree[this->get_right(node)])
        ) {
            child_node = this->get_right(node);
        }

        if ((!this->is_min_heap && tree[node] >= tree[child_node]) 
            || (this->is_min_heap && tree[node] <= tree[child_node])
        ) {
            return;
        }

        swap(tree[node], tree[child_node]);

        fix_pop(child_node);
    }
};
```

---