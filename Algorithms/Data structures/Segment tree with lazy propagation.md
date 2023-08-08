> [!info] Objetivo
> - Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre um intervalo $[L, R]$ ou fazer um range update em um intervalo qualquer. Essas perguntas no intervalo podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

```cpp
#define L(x) (x << 1)
#define R(x) (L(x) | 1)

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

	// l and r has to be on the interval [1..N]
	void update(int l, int r, U v) {
		this->update(1, 1, this->n, l, r, v);
	}

	// Accept queries on the interval [1..N]
    T query(int l, int r) {
	    // Return the property in the Node that is the answer
    }

private:
	struct Node {
		T lazy;
		// Node variables and constructor initialization

		void add_lazy(T v) {
			// Lazy aggregation logic
		}

		T apply_lazy() {
			// Lazy application logic and reset the lazyness
		}

		Node operator+(const Node &o) const {
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

        this->build(v, L(node), l, mid);
        this->build(v, R(node), mid + 1, r);

        this->tree[node] = this->tree[L(node)] + this->tree[R(node)];
    }

	void lazy_propagation(int node, int l, int r) {
        if (this->tree[node].lazy == 0) {
            return;
        }

		T lazy {this->tree[node].apply_lazy()};

        if (l < r) {
	        this->tree[L(node)].add_lazy(lazy);
	        this->tree[R(node)].add_lazy(lazy);
        }
    }

	void update(int node, int l, int r, int l_target, int r_target, T v) {
        this->lazy_propagation(node, l, r);

        if (r_target < l || r < l_target) {
            return;
        }

        if (l_target <= l && r <= r_target) {
	        this->tree[node].add_lazy(v);

            this->lazy_propagation(node, l, r);

            return;
        }

        int mid {(l + r) / 2};

        this->update(L(node), l, mid, l_target, r_target, v);
        this->update(R(node), mid + 1, r, l_target, r_target, v);

        this->tree[node] = this->tree[L(node)] + this->tree[R(node)];
    }

	Node query(int node, int l, int r, int l_target, int r_target) {
        this->lazy_propagation(node, l, r);

		if (l == l_target && r == r_target) {
			return this->tree[node];
		}

        int mid {(l + r) / 2};
    
		if (r_target <= mid) {
			return this->query(L(node), l, mid, l_target, r_target);
		}

		if (l_target > mid) {
			return this->query(R(node), mid + 1, r, l_target, r_target);
		}

        return this->query(L(node), l, mid, l_target, mid) + this->query(R(node), mid + 1, r, mid + 1, r_target);
    }
};
```

---