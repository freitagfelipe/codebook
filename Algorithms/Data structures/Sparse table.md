> [!info] Objetivo
> - Responder $Q$ perguntas de intervalo $[L, R]$ de maneira eficiente em um vetor $V$. Essas $Q$ perguntas podem, por exemplo, estar relacionada um dos seguintes assuntos: mínimo, máximo, etc.

> [!caution] Restrições
> - O vetor não pode mudar durante as perguntas.
> - A função utilizada na sparse table deve aceitar sobreposições, pois as vezes pode acontecer de os intervalos utilizados durante a query da sparse table não serem disjuntos. Caso a função utilizada não aceite sobreposições o que se deve fazer é dividir o intervalo nos maiores logs possíveis. 

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Query: $O(1)$

```cpp
template <typename T>
class SparseTable {
public:
    SparseTable(auto fn) {
        this->fn = fn;
    }

    void build(int n, T *v) {
        this->logs.resize(n + 1);

        this->logs[1] = 0;

        for (int i {2}; i <= n; ++i) {
            this->logs[i] = this->logs[i / 2] + 1;
        }

        this->arr.resize(n, vector<int>(this->logs[n] + 1));

        for (int i {}; i < n; ++i) {
            this->arr[i][0] = v[i];
        }

        for (int k {1}; (1 << k) <= n; ++k) {
            for (int i {}; i + (1 << k) - 1 < n; ++i) {
                this->arr[i][k] = this->fn(this->arr[i][k - 1], this->arr[i + (1 << (k - 1))][k - 1]);
            }
        }
    }

    int query(int l, int r) {
        int size {r - l + 1};
        int k {this->logs[size]};

        return this->fn(this->arr[l][k], this->arr[r - (1 << k) + 1][k]);
    }
    
private:
    vector<int> logs;
    vector<vector<T>> arr;
    auto fn;
};
```

---