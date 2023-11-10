> [!info] Objetivo
> - A merge sort tree tem como objetivo permitir consultas em intervalos da merge sort tree.

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Less/greater/equal than: $O(\log^2 n)$

```cpp
typedef long long ll;

#define L(x) (x << 1)
#define R(x) (L(x) | 1)
#define all(x) x.begin(), x.end()

// T is the type that the Node will store
template <typename T>
class MergeSortTree {
public:
    MergeSortTree(const vector<T> &v) {
        this->n = (int) v.size();

        this->tree.resize(this->n * 4);

        this->build(v, 1, 1, this->n);
    }

    int lt(int l, int r, int k) {
        return this->lt(1, 1, this->n, l, r, k);
    }

    int eq(int l, int r, int k) {
        return this->eq(1, 1, this->n, l, r, k);
    }

    int gt(int l, int r, int k) {
        return this->gt(1, 1, this->n, l, r, k);
    }

private:
    typedef vector<T> Node;
    
    vector<Node> tree;
    int n;

    // l has to be on the interval [1..N]
	// Because of that we need to do l - 1
	// To match the interval of v that goes from [0..N - 1]
    void build(const vector<T> &v, int node, int l, int r) {
        if (l == r) {
            this->tree[node].push_back(v[l - 1]);

            return;
        }

        int mid {(l + r) / 2};

        this->build(v, L(node), l, mid);
        this->build(v, R(node), mid + 1, r);

        merge(all(this->tree[L(node)]), all(this->tree[R(node)]), back_inserter(this->tree[node]));
    }

    int lt(int node, int l, int r, int l_target, int r_target, int k) {
        if (l == l_target && r == r_target) {
            return lower_bound(all(this->tree[node]), k) - this->tree[node].begin();
        }

        int mid {(l + r) / 2};

        if (r_target <= mid) {
            return this->lt(L(node), l, mid, l_target, r_target, k);
        }

        if (l_target > mid) {
            return this->lt(R(node), mid + 1, r, l_target, r_target, k);
        }

        return this->lt(L(node), l, mid, l_target, mid, k) + this->lt(R(node), mid + 1, r, mid + 1, r_target, k);
    }

    int eq(int node, int l, int r, int l_target, int r_target, int k) {
        if (l == l_target && r == r_target) {
            return upper_bound(all(this->tree[node]), k) - lower_bound(all(this->tree[node]), k);
        }

        int mid {(l + r) / 2};

        if (r_target <= mid) {
            return this->eq(L(node), l, mid, l_target, r_target, k);
        }

        if (l_target > mid) {
            return this->eq(R(node), mid + 1, r, l_target, r_target, k);
        }

        return this->eq(L(node), l, mid, l_target, mid, k) + this->eq(R(node), mid + 1, r, mid + 1, r_target, k);
    }

    int gt(int node, int l, int r, int l_target, int r_target, int k) {
        if (l == l_target && r == r_target) {
            return this->tree[node].end() - upper_bound(all(this->tree[node]), k);
        }

        int mid {(l + r) / 2};

        if (r_target <= mid) {
            return this->gt(L(node), l, mid, l_target, r_target, k);
        }

        if (l_target > mid) {
            return this->gt(R(node), mid + 1, r, l_target, r_target, k);
        }

        return this->eq(L(node), l, mid, l_target, mid, k) + this->gt(R(node), mid + 1, r, mid + 1, r_target, k);
    }
};
```

---