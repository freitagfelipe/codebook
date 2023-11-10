> [!info] Objetivo
> - O union-find com rollback possui o mesmo objetivo do [[Union-find]], porém essa implementação permite com que seja possível desfazer operações de união. Entretanto, para atingir esse feito é necessário remover a compressão de caminho da função find.

> [!note]- Complexidade
> - Find/merge: $O(\log n)$
> - Rollback: $O(t)$
> - Time: $O(1)$

```cpp
class UnionFindRB {
public:
    UnionFindRB(int n) {
        this->n = n;
        this->p.assign(n, 0);
        this->h.assign(n, 0);

        iota(this->p.begin(), this->p.end(), 1);
    }

    int find(int x) {
        if (this->p[x] == x) {
            return x;
        }

        return this->find(this->p[x]);
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

        this->op.emplace_back(x, this->h[x], y, this->p[y]);

        this->p[y] = x;

        if (this->h[x] == this->h[y]) {
            ++this->h[x];
        }
    }

    // Undo the operations until only t operations are left
    void rollback(int t) {
	    while ((int) op.size() > t) {
		    auto [x, hx, y, py] = op.back();

		    h[x] = hx;
		    p[y] = py;

		    op.pop_back();
	    }	
    }

    // Return how many operations were done
    int time() {
	    return (int) op.size();
    }

private:
    int n;
    vector<int> p;
    vector<int> h;
    vector<tuple<int, int, int, int>> op;
};
```

---