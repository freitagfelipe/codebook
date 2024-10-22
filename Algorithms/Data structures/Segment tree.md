> [!info] Objetivo
> - A segment tree tem como objetivo realizar de maneira eficiente operações que consistem em consultas em intervalo e atualizações em índice.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

```cpp
#define L(x) (x << 1)
#define R(x) (L(x) | 1)

// T is the type that the Node will store
// U is the type of the operations of update
template <typename T, typename U>
class SegmentTree {
public:
	// This constructor can be used when the build step is not required
	SegmentTree(int n) {
        this->n = n;

        this->tree.resize(this->n * 4);
	}

	SegmentTree(const vector<U> &v) {
        this->n = (int) v.size();

        this->tree.resize(this->n * 4);

        this->build(v, 1, 1, this->n);
	}

	// target_node has to be on the interval [1..N]
    void update(int target_node, U v) {
        this->update(1, 1, this->n, target_node, v);
    }

	// Accept queries on the interval [1..N]
    T query(int l, int r) {
	    // Return the property in the node that is the answer
    }

private:
    struct Node {
		// Node variables

		Node() = default;

        Node operator+(const Node &o) const {
            // Node merge logic
        }
    };

    int n;
    vector<Node> tree;

	// l has to be on the interval [1..N]
	// Because of that we need to do l - 1
	// To match the interval of v that goes from [0..N - 1]
    void build(const vector<U> &v, int node, int l, int r) {
        if (l == r) {
	        // Build tree logic

            return;
        }

        int mid {(l + r) / 2};

        this->build(v, L(node), l, mid);
        this->build(v, R(node), mid + 1, r);

        this->tree[node] = this->tree[L(node)] + this->tree[R(node)];
    }

    void update(int node, int l, int r, int target, U v) {
        if (l == r) {
            // Update tree logic

            return;
        }

        int mid {(l + r) / 2};

        if (target <= mid) {
            this->update(L(node), l, mid, target, v);
        } else {
            this->update(R(node), mid + 1, r, target, v);
        }

        this->tree[node] = this->tree[L(node)] + this->tree[R(node)];
    }

    Node query(int node, int l, int r, int l_target, int r_target) {
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