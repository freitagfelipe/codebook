```ad-info
title: Objetivo

- Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre um intervalo $[L, R]$ ou fazer um range update em um intervalo qualquer. Essas perguntas no intervalo podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc.
```

```ad-note
title: Complexidade
collapse: true

- Build: $O(n)$
- Update: $O(\log n)$
- Query: $O(\log n)$
```

`````ad-example
title: Segment tree with lazy propagation para fazer $Q$ operações em um intervalo $[L, R]$

- No exemplo a baixo as operações são somar um valor v em um intervalo e dizer a soma do intervalo $[L,R]$.

⠀
```cpp
class Node {
public: 
    Node(int s = 0) {
        this->sum = s;
    }

    int operator+(const Node &other) {
        return this->sum + other.sum;
    }

    friend class SegmentTree;
private:
    int sum;
    int lazy {};
};

class SegmentTree {
public:
    void build(int n, int *v) {
        this->n = n;

        arr.resize(n + 1);
        tree.resize(4 * n);

        this->build(v, 1, 1, n);
    }

    void update(int p, int q, int v) {
        this->update(1, 1, this->n, p, q, v);
    }

    int query(int p, int q) {
        return this->query(1, 1, n, p, q);
    }

private:
    int n;
    vector<int> arr;
    vector<Node> tree;

    void build(int *v, int node, int l, int r) {
        if (l == r) {
            this->arr[l] = v[l];

            this->tree[node].sum = v[l];

            return;
        }

        int mid {(l + r) / 2};

        this->build(v, node * 2, l, mid);
        this->build(v, node * 2 + 1, mid + 1, r);

        this->tree[node].sum = this->tree[node * 2] + this->tree[node * 2 + 1];
    }

    void lazy_propagation(int node, int l, int r) {
        if (this->tree[node].lazy == 0) {
            return;
        }

        this->tree[node].sum += (r - l + 1) * this->tree[node].lazy;

        if (l < r) {
            this->tree[node * 2].lazy += this->tree[node].lazy;
            this->tree[node * 2 + 1].lazy += this->tree[node].lazy;
        }

        this->tree[node].lazy = 0;
    }

    void update(int node, int l, int r, int p, int q, int v) {
        if (q < l || r < p) {
            return;
        }
    
        this->lazy_propagation(node, l, r);

        if (p <= l && r <= q) {
            this->tree[node].lazy += v;

            this->lazy_propagation(node, l, r);

            return;
        }

        int mid {(l + r) / 2};

        this->update(node * 2, l, mid, p, q, v);
        this->update(node * 2 + 1, mid + 1, r, p, q, v);

        this->tree[node].sum = this->tree[node * 2] + this->tree[node * 2 + 1];
    }

    int query(int node, int l, int r, int p, int q) {
        if (q < l || r < p) {
            return 0;
        }

        this->lazy_propagation(node, l, r);
        
        if (p <= l && r <= q) {
            return tree[node].sum;
        }

        int mid {(l + r) / 2};

        return this->query(node * 2, l, mid, p, q) + this->query(node * 2 + 1, mid + 1, r, p, q);
    }
};
```
`````

---