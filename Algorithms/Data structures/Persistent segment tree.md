> [!info] Objetivo
> - O objetivo da [[Segment tree]] continua o mesmo, mas agora com a adição de persistência que permite que novas versões da estrutura sejam criados e permite que versões passadas sejam consultadas sem perder as informações da versão atual.

> [!note]- Complexidade
> - Build: $O(n)$
> - Update: $O(\log n)$
> - Query: $O(\log n)$

```cpp
// T is the type that the Node and the QueryAnswer will store
// U is the type of the operations of update
template <typename T, typename U>
class PersistentSegmentTree {
public:
	PersistentSegmentTree(int n) {
        this->n = n;

        this->states.push_back(this->build({}, 1, this->n));
    }

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

        this->states[state] = this->update(this->states[state], 1, this->n, target_node, v);
    }

	// Accept queries on the interval [1..N]
	// The state must be on the interval of [0..states_size - 1]
    T query(int state, int l, int r) {
        if (state < 0 || state >= (int) states.size()) {
            throw runtime_error("Invalid state");
        }

        QueryAnswer qa {this->query(this->states[state], 1, this->n, l, r)};

	    // Return the property in the query answer that is the answer
    }

	// Create a state based on another state
	// The state must be on the interval of [0..states_size - 1]
	void create_state(int state) {
		this->states.push_back(this->states[state]);
	}

    size_t states_size() {
        return this->states.size();
    }

private:
    struct Node {
        Node *left {};
        Node *right {};

        // Node variables
        
        Node() = default;

        Node(Node *left, Node *right) {
            this->left = left;
            this->right = right;

            if (left != nullptr) {
                // Node merge logic
            }

            if (right != nullptr) {
                // Node merge logic
            }
        }
    };

    struct QueryAnswer {
        // Query answer variables
        
        QueryAnswer operator+(const QueryAnswer &o) const {
            // QueryAnswer merge logic
        }
    };

    int n;
    vector<Node*> states;

    // l has to be on the interval [1..N]
	// Because of that we need to do l - 1
	// To match the interval of v that goes from [0..N - 1]
    Node *build(const vector<U> &v, int l, int r) {
        if (l == r) {
            Node *node {new Node()};
            
	        if (v.size() == 0) {
		        return node;
	        }

	        // Setup node logic

            return node;
        }

        int mid {(l + r) / 2};

        return new Node(this->build(v, l, mid), this->build(v, mid + 1, r));
    }

    Node *update(Node *node, int l, int r, int target, U v) {
        if (l == r) {
            Node *node {new Node()};

            // Create node logic

            return node;
        }

        int mid {(l + r) / 2};

        if (target <= mid) {
            return new Node(this->update(node->left, l, mid, target, v), node->right);
        }

        return new Node(node->left, this->update(node->right, mid + 1, r, target, v));
    }

    QueryAnswer query(Node *node, int l, int r, int l_target, int r_target) {
        if (l == l_target && r == r_target) {
            QueryAnswer qa;

            // Setup query answer logic
            
            return qa;
        }

		int mid {(l + r) / 2};

		if (r_target <= mid) {
		    return this->query(node->left, l, mid, l_target, r_target);
		}

		if (l_target > mid) {
		    return this->query(node->right, mid + 1, r, l_target, r_target);
		}

		return this->query(node->left, l, mid, l_target, mid) + this->query(node->right, mid + 1, r, mid + 1, r_target);
    }
};
```

---