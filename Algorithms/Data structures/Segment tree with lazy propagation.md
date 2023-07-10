> [!info] Objetivo
> - Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre um intervalo $[L, R]$ ou fazer um range update em um intervalo qualquer. Essas perguntas no intervalo podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

```cpp
template <typename T, typename U>
class SegmentTree {
public:
	void build(int n, U *v) {
		this->n = n;

		this->arr.resize(n + 1);
		this->tree.resize(n * 4);

		this->build(v, 1, 1, n);
	}

	// l and r has to be on the interval [1..N]
	void update(int l, int r, U v) {
		this->update(1, 1, this->n, l, r, v);
	}

	// Accept queries on the interval [1..N]
    T query(int l, int r) {
        return this->query(1, 1, this->n, l, r).sum;
    }

private:
	struct Node {
		T lazy;
		// Node variables and constructor initialization

		void add_lazy(T v) {
			// Lazy aggregation logic
		}

		T apply_lazy() {
			// Lazy application logic and reset
		}

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
	void build(int *v, int node, int l, int r) {
        if (l == r) {
            // Build tree and arr logic

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

		T lazy {this->tree[node].apply_lazy()};

        if (l < r) {
	        this->tree[node * 2].add_lazy(lazy);
	        this->tree[node * 2 + 1].add_lazy(lazy);
        }
    }

	void update(int node, int l, int r, int p, int q, T v) {
        this->lazy_propagation(node, l, r);

        if (q < l || r < p) {
            return;
        }

        if (p <= l && r <= q) {
	        this->tree[node].add_lazy(v);

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

---