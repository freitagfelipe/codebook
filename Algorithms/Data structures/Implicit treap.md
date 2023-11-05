> [!info] Objetivo
> - Essa estrutura é feita a partir de uma modificação da [[Treap]] e tem como objetivo ser um vetor poderoso, capaz de inserir/remover elementos em qualquer índice, aceitar consultas em intervalo, aceitar atualizações em range e tudo isso com ótima complexidade.

> [!note]- Complexidade
> - Split: $O(\log n)$
> - Merge: $O(\log n)$

```cpp
#define IPTreapNull -1

typedef long long ll;
typedef int IPTreap;

mt19937 rng((int) chrono::steady_clock::now().time_since_epoch().count());

template <typename T = int>
struct ITreap {
    ll priority;
    array<int, 2> children {IPTreapNull, IPTreapNull};
    int subtree_size {1};
    T data {};
    T lazy {};

    // ITreap variables

    ITreap(T data) {
        this->data = data;
        this->priority = rng();
    }
};

vector<ITreap<>> treaps;

int size(IPTreap t) {
    return t == IPTreapNull ? 0 : treaps[t].subtree_size;
}

void recalculate(IPTreap t) {
    if (t == IPTreapNull) {
        return;
    }

    auto &treap {treaps[t]};

    treap.subtree_size = 1;

    // Update ITreap variables here

    for (IPTreap child : treap.children) {
        if (child == IPTreapNull) {
            continue;
        }

        treap.subtree_size += treaps[child].subtree_size;

        // Update ITreap variables here
    }
}

void apply_lazy(IPTreap t) {
    if (t == IPTreapNull || treaps[t].lazy == 0) {
        return;
    }

    auto &treap {treaps[t]};

    for (IPTreap child : treap.children) {
        if (child == IPTreapNull) {
            continue;
        }

        treaps[child].lazy += treap.lazy;
    }

    // Update ITreap data based on lazy

    treap.lazy = 0;

    recalculate(t);
}

// The left ITreap will have size of left_size and the right
// ITreap will have the remainder
pair<IPTreap, IPTreap> split(IPTreap t, int left_size) {
    if (t == IPTreapNull) {
        return {IPTreapNull, IPTreapNull};
    }

    apply_lazy(t);

    auto &treap {treaps[t]};

    if (size(treap.children[0]) >= left_size) {
        auto [left, right] {split(treap.children[0], left_size)};

        treap.children[0] = right;

        recalculate(t);

        return {left, t};
    }

    left_size -= size(treap.children[0]) + 1;

    auto [left, right] {split(treap.children[1], left_size)};

    treap.children[1] = left;
    
    recalculate(t);

    return {t, right};
}

IPTreap merge(IPTreap l, IPTreap r) {
    if (l == IPTreapNull || r == IPTreapNull) {
        return l == IPTreapNull ? r : l;
    }

    apply_lazy(l);
    apply_lazy(r);

    auto &lt {treaps[l]}, &rt {treaps[r]};

    IPTreap treap {};

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
```

---