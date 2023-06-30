> [!info] Objetivo
> - Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre um intervalo $[L, R]$ ou fazer um point update em um índice qualquer. Essas perguntas no intervalo podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc. A parte da estrutura que muda junto com a necessidade da questão é a classe Node.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

```cpp
// T is the type that the Node will store
// U is the type that the array will store
template <typename T, typename U>
class SegmentTree {
public:
    void build(int n, U *v) {
        this->n = n;

        this->arr.resize(n + 1);
        this->tree.resize(n * 4);

        this->build(v, 1, 1, n);
    }

	// target_node has to be on the interval [1..N]
    void update(int target_node, U v) {
        this->update(1, 1, this->n, target_node, v);
    }

	// Accept queries on the interval [1..N]
    T query(int l, int r) {
        return this->query(1, 1, this->n, l, r).minv;
    }
private:
    struct Node {
		// Node variables and constructor initialization

        Node operator+(const Node &o) {
            // Node merge logic
        }
    };

    int n;
    vector<U> arr;
    vector<Node> tree;

	// l has to be on the interval [1..N]
	// Because of that we need to do l - 1
	// To match the interval of v that goes from [0..N - 1]
    void build(U *v, int node, int l, int r) {
        if (l == r) {
	        // Build tree and arr logic

            return;
        }

        int mid {(l + r) / 2};

        this->build(v, node * 2, l, mid);
        this->build(v, node * 2 + 1, mid + 1, r);

        this->tree[node] = this->tree[node * 2] + this->tree[node * 2 + 1];
    }

    void update(int node, int l, int r, int target_node, U v) {
        if (l == r) {
            // Update tree and arr logic

            return;
        }

        int mid {(l + r) / 2};

        if (target_node <= mid) {
            this->update(node * 2, l, mid, target_node, v);
        } else {
            this->update(node * 2 + 1, mid + 1, r, target_node, v);
        }

        this->tree[node] = this->tree[node * 2] + this->tree[node * 2 + 1];
    }

    Node query(int node, int l, int r, int l_target, int r_target) {
        if (r_target < l || r < l_target) {
            return Node();
        } else if (l_target <= l && r <= r_target) {
            return this->tree[node];
        }

        int mid {(l + r) / 2};

        return this->query(node * 2, l, mid, l_target, r_target) + this->query(node * 2 + 1, mid + 1, r, l_target, r_target);
    }
};
```

---