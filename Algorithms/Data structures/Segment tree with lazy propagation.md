> [!info] Objetivo
> - Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre um intervalo $[L, R]$ ou fazer um range update em um intervalo qualquer. Essas perguntas no intervalo podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

`````ad-example
title: Segment tree with lazy propagation para fazer $Q$ operações de somar $x$ em cada valor de um intervalo $[L, R]$ ou responder qual a soma de um intervalo $[L, R]$.

```cpp
template <typename T>
class SegmentTree {
public:
    void build(int n, int *v) {
        this->n = n;

        this->arr.resize(n + 1);
        this->tree.resize(4 * n);

        this->build(v, 1, 1, n);
    }

	// l and r has to be on the interval [1..N]
    void update(int l, int r, T v) {
        this->update(1, 1, this->n, l, r, v);
    }

	// Accept queries on the interval [1..N]
    T query(int l, int r) {
        return this->query(1, 1, this->n, l, r).sum;
    }

private:
    struct Node {
        T sum;
        T lazy;

        Node(T s = 0) {
            this->sum = s;
            this->lazy = 0;
        }

        Node operator+(const Node &other) {
            return Node(this->sum + other.sum);
        }
    };

    int n;
    vector<T> arr;
    vector<Node> tree;

	// l has to be on the interval [1..N]
	// Because of that we need to do l - 1
	// To match the interval of v that goes from [0..N - 1]
    void build(int *v, int node, int l, int r) {
        if (l == r) {
            this->arr[l] = v[l - 1];

            this->tree[node].sum = v[l - 1];

            return;
        }

        int mid {(l + r) / 2};

        this->build(v, node * 2, l, mid);
        this->build(v, node * 2 + 1, mid + 1, r);

        this->tree[node] = this->tree[node * 2] + this->tree[node * 2 + 1];
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

    void update(int node, int l, int r, int p, int q, T v) {
        this->lazy_propagation(node, l, r);

        if (q < l || r < p) {
            return;
        }

        if (p <= l && r <= q) {
            this->tree[node].lazy += v;

            this->lazy_propagation(node, l, r);

            return;
        }

        int mid {(l + r) / 2};

        this->update(node * 2, l, mid, p, q, v);
        this->update(node * 2 + 1, mid + 1, r, p, q, v);

        this->tree[node] = this->tree[node * 2] + this->tree[node * 2 + 1];
    }

    Node query(int node, int l, int r, int p, int q) {
        if (q < l || r < p) {
            return Node();
        }

        this->lazy_propagation(node, l, r);
        
        if (p <= l && r <= q) {
            return tree[node];
        }

        int mid {(l + r) / 2};

        return this->query(node * 2, l, mid, p, q) + this->query(node * 2 + 1, mid + 1, r, p, q);
    }
};
```
`````

---