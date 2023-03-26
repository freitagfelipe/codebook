```ad-info
title: Objetivo

- Fazer de maneira eficiente $Q$ operações que podem consistir em perguntar algo sobre um intervalo $[L, R]$ ou fazer um point update em um índice qualquer. Essas perguntas no intervalo podem, por exemplo, estar relacionada a um dos seguintes temas: mínimo, máximo, etc. A parte da estrutura que muda junto com a necessidade da questão é a classe Node.
```

```ad-hint
title: Observação

- O conteúdo que a classe Node guarda depende do que a questão está pedindo, no exemplo abaixo ela quer a soma do intervalo $[L, R]$.
```

```ad-note
title: Complexidade
collapse: true

- Build: $O(n)$
- Update: $O(\log n)$
- Query: $O(\log n)$
```

`````ad-example
title: Segment tree para fazer $Q$ operações de somar um valor $v$ em $v_i$ ou responder a soma de todos os elementos no intervalo $[L, R]$.

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

    // target_node tem que pertencer ao intervalo [1..N]
    void update(int target_node, T v) {
        this->update(1, 1, this->n, target_node, v);
    }

    // Queries no intervalo [1..N]
    T query(int l, int r) {
        return this->query(1, 1, this->n, l, r).sum;
    }

private:
    struct Node {
        T sum;

        Node(T s = 0) {
            this->sum = s;
        }

        Node operator+(const Node &other) {
            return Node(this->sum + other.sum);
        }
    };

    int n;
    vector<T> arr;
    vector<Node> tree;

    // l pertence ao intervalo [1..N]
    // Por isso precisamos fazer l - 1
    // Para coincidir com o intervalo de v que vai de [0..N - 1]
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

    void update(int node, int l, int r, int target_node, T v) {
        if (l == r) {
            this->arr[target_node] += v;

            this->tree[node].sum += v;

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
            return tree[node];
        }

        int mid {(l + r) / 2};

        return this->query(node * 2, l, mid, l_target, r_target) + this->query(node * 2 + 1, mid + 1, r, l_target, r_target);
    }
};
```
`````

---