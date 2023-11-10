> [!info] Objetivo
> - A Treap é uma estrutura criada a partir da junção da [[Binary search tree (BST)]] e da [[Binary heap]] e tem como objetivo ser uma árvore randomicamente balanceada.

> [!note]- Complexidade
> - Split/split by size: $O(\log n)$
> - Merge: $O(\log n)$
> - Search/insert/remove: $O(\log n)$

```cpp
#define PTreapNull -1

typedef long long ll;
typedef int PTreap;

mt19937 rng((int) chrono::steady_clock::now().time_since_epoch().count());

template <typename T = int>
struct Treap {
    ll priority;
    array<int, 2> children {PTreapNull, PTreapNull};
    int subtree_size {1};
    T data {};
    T lazy {};

    // Treap variables

    Treap(T data) {
        this->data = data;
        this->priority = rng();
    }
};

vector<Treap<>> treaps;

int size(PTreap t) {
    return t == PTreapNull ? 0 : treaps[t].subtree_size;
}

void recalculate(PTreap t) {
    if (t == PTreapNull) {
        return;
    }

    auto &treap {treaps[t]};

    treap.subtree_size = 1;

    // Update Treap variables here

    for (PTreap child : treap.children) {
        if (child == PTreapNull) {
            continue;
        }

        treap.subtree_size += treaps[child].subtree_size;

        // Update Treap variables here
    }
}

void apply_lazy(PTreap t) {
    if (t == PTreapNull || treaps[t].lazy == 0) {
        return;
    }

    auto &treap {treaps[t]};

    for (PTreap child : treap.children) {
        if (child == PTreapNull) {
            continue;
        }

        treaps[child].lazy += treap.lazy;
    }

    // Update Treap data based on lazy

    treap.lazy = 0;

    recalculate(t);
}

// The left Treap will have size of left_size and the right
// Treap will have the remainder
pair<PTreap, PTreap> split_by_size(PTreap t, int left_size) {
    if (t == PTreapNull) {
        return {PTreapNull, PTreapNull};
    }

    apply_lazy(t);

    auto &treap {treaps[t]};

    if (size(treap.children[0]) >= left_size) {
        auto [left, right] {split_by_size(treap.children[0], left_size)};

        treap.children[0] = right;

        recalculate(t);

        return {left, t};
    }

    left_size -= size(treap.children[0]) + 1;

    auto [left, right] {split_by_size(treap.children[1], left_size)};

    treap.children[1] = left;
    
    recalculate(t);

    return {t, right};
}

// All the elements of the left Treap will have data <= key
// and all elements of the right Treap will have data > key
pair<PTreap, PTreap> split(PTreap t, int key) {
    if (t == PTreapNull) {
        return {PTreapNull, PTreapNull};
    }

    apply_lazy(t);

    auto &treap {treaps[t]};

    if (treap.data <= key) {
        auto [left, right] {split(treap.children[1], key)};

        treap.children[1] = left;

        recalculate(t);

        return {t, right};
    }

    auto [left, right] {split(treap.children[0], key)};

    treap.children[0] = right;

    recalculate(t);

    return {left, t};
}

PTreap merge(PTreap l, PTreap r) {
    if (l == PTreapNull || r == PTreapNull) {
        return l == PTreapNull ? r : l;
    }

    apply_lazy(l);
    apply_lazy(r);

    auto &lt {treaps[l]}, &rt {treaps[r]};

    PTreap treap {};

    if (lt.priority < rt.priority) {
        lt.children[1] = merge(lt.children[1], r);

        treap = l;
    } else {
        rt.children[0] = merge(l, rt.children[0]);

        treap = r;
    }

    recalculate(treap);

    return treap;
}

template <typename T>
PTreap remove(PTreap t, T key) {
    if (t == PTreapNull) {
        return PTreapNull;
    }

    auto &treap {treaps[t]};

    if (treap.data == key) {
        return merge(treap.children[0], treap.children[1]);
    }

    if (key < treap.data) {
        treap.children[0] = remove(treap.children[0], key);
    } else {
        treap.children[1] = remove(treap.children[1], key);
    }

    return t;
}

template <typename T>
PTreap insert(PTreap t, T key) {
    if (t == PTreapNull) {
        return PTreapNull;
    }

    PTreap ot {(int) treaps.size()};

    treaps.emplace_back(key);

    auto [left, right] {split(t, key)};

    return merge(merge(left, ot), right);
}

template <typename T>
PTreap search(PTreap t, T key) {
    if (t == PTreapNull) {
        return PTreapNull;
    }

    auto &treap {treaps[t]};

    if (treap.data == key) {
        return t;
    }

    return search(key < treap.data ? treap.children[0] : treap.children[1], key);
}
```

---