> [!info] Objetivo
> - O union-find tem como objetivo gerenciar uma coleção de conjuntos disjuntos, onde cada conjunto contém elementos distintos. Ele fornece operações eficientes para realizar união de conjuntos e encontrar a representação de um elemento dentro de um conjunto.

> [!note]- Complexidade
> - Find/join: $O(\alpha(n))$

```cpp
class UnionFind {
public:
    UnionFind(int n) {
        this->n = n;
        this->p.assign(n, 0);
        this->h.assign(n, 0);

        iota(this->p.begin(), this->p.end(), 1);
    }

    int find(int x) {
        if (this->p[x] == x) {
            return x;
        }

        return this->p[x] = this->find(this->p[x]);
    }

    void join(int x, int y) {
        x = this->find(x);
        y = this->find(y);

        if (x == y) {
            return;
        }

        if (this->h[x] < this->h[y]) {
            swap(x, y);
        }

        this->p[y] = x;

        if (this->h[x] == this->h[y]) {
            ++this->h[x];
        }
    }

private:
    int n;
    vector<int> p;
    vector<int> h;
};
```

---