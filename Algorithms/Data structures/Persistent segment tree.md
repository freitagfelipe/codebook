> [!info] Objetivo
> - O objetivo da [[Segment tree]] continua o mesmo, mas agora com a adição de persistência que permite que novas versões da estrutura sejam criados e permite que versões passadas sejam consultadas e alteradas sem perder as informações da versão atual.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

```cpp
// T is the type that the Node will store
// U is the type of the operations of update
template <typename T, typename U>
class PersistentSegmentTree {
public:
    PersistentSegmentTree(const vector<U> &v) {
        this->n = (int) v.size();

        this->states.push_back(this->build(v, 1, this->n));
    }

    // target_node has to be on the interval [1..N]
	// The state must be on the interval of [0..states_size - 1]
	// It will update the choosen state with the update
    void update(int state, int target_node, U v) {
        if (state < 0 || state >= (int) states.size()) {
            throw runtime_error("Invalid state");
        }

		// This can be changed with
		// this->states.push_back(this->update(this->states[state], 1, this->n, target_node, v));
		// To create an another state after the update rather then overwrite the previous state
        this->states[state] = this->update(this->states[state], 1, this->n, target_node, v);
    }

	// Accept queries on the interval [1..N]
	// The state must be on the interval of [0..states_size - 1]
    T query(int state, int l, int r) {
        if (state < 0 || state >= (int) states.size()) {
            throw runtime_error("Invalid state");
        }
        
        // Return the property in the node that is the answer
    }

	// Create a state based on another state
	// The state must be on the interval of [0..states_size - 1]
	void create_state(int state) {
        if (state < 0 || state >= (int) states.size()) {
            throw runtime_error("Invalid state");
        }

		this->states.push_back(this->states[state]);
	}

    size_t states_size() {
        return this->states.size();
    }

private:
    struct Node {
        int left {-1};
        int right {-1};

        // Node variables
        
        Node() = default;

        Node operator+(const Node &o) const {
            // Node merge logic
        }
    };

    int n;
    vector<int> states;
    vector<Node> nodes;

    // l has to be on the interval [1..N]
	// Because of that we need to do l - 1
	// To match the interval of v that goes from [0..N - 1]
    int build(const vector<U> &v, int l, int r) {
        if (l == r) {
            Node n;

	        // Setup node logic

            this->nodes.push_back(n);

            return (int) this->nodes.size() - 1;
        }

        int mid {(l + r) / 2};
        int ret_idx {(int) this->nodes.size()};

        this->nodes.emplace_back();

        int left_idx {this->build(v, l, mid)};
        int right_idx {this->build(v, mid + 1, r)};

        this->nodes[ret_idx] = this->nodes[left_idx] + this->nodes[right_idx];
        this->nodes[ret_idx].left = left_idx;
        this->nodes[ret_idx].right = right_idx;

        return ret_idx;
    }

    int update(int node, int l, int r, int target, U v) {
        if (l == r) {
            Node n;

            // Update node logic

            this->nodes.push_back(n);

            return (int) this->nodes.size() - 1;
        }

        int mid {(l + r) / 2};
        int ret_idx {(int) this->nodes.size()};

        this->nodes.emplace_back();

        int left_idx {};
        int right_idx {};

        if (target <= mid) {
            left_idx = this->update(this->nodes[node].left, l, mid, target, v);
            right_idx = this->nodes[node].right;
        } else {
            left_idx = this->nodes[node].left;
            right_idx = this->update(this->nodes[node].right, mid + 1, r, target, v);
        }

        this->nodes[ret_idx] = this->nodes[left_idx] + this->nodes[right_idx];
        this->nodes[ret_idx].left = left_idx;
        this->nodes[ret_idx].right = right_idx;

        return ret_idx;
    }

    Node query(int node, int l, int r, int l_target, int r_target) {
        if (l == l_target && r == r_target) {
            return this->nodes[node];
        }

		int mid {(l + r) / 2};

		if (r_target <= mid) {
		    return this->query(this->nodes[node].left, l, mid, l_target, r_target);
		}

		if (l_target > mid) {
		    return this->query(this->nodes[node].right, mid + 1, r, l_target, r_target);
		}

		return this->query(this->nodes[node].left, l, mid, l_target, mid) + this->query(this->nodes[node].right, mid + 1, r, mid + 1, r_target);
    }
};
```

---