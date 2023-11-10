> [!info] Objetivo
> - A sparse table consegue responder consultas em intervalos em tempo constante, mas com uma etapa de construção um pouco mais custosa.

> [!caution] Restrições
> - O vetor não pode mudar durante as consultas.
> - A função utilizada na sparse table deve ser idempotente. Caso a função utilizada não seja idempotente o que se deve fazer é dividir o intervalo nos maiores logs possíveis e com isso realizar a consulta com uma complexidade $O(\log n)$.

> [!note]- Complexidade
> - Build: $O(n \log n)$
> - Query: $O(1)$

```cpp
template <typename T>
class SparseTable {
public:
    SparseTable(const vector<T> &v, const function<T(T, T)> &fn) {
        this->fn = fn;

        this->build(v.size(), v);
    }

    // Accept queries on the range [0..N - 1]
    T query(int l, int r) {
	    // If using C++20 this can be calculated in O(1)
	    // with bit_width avoiding cache misses caused by the logs vector
        int size {r - l + 1};
        int k {this->logs[size]};

        return this->fn(this->arr[l][k], this->arr[r - (1 << k) + 1][k]);
    }
    
private:
    vector<int> logs;
    vector<vector<T>> arr;
    function<T(T, T)> fn;

    void build(int n, const vector<T> &v) {
        this->logs.resize(n + 1);

        this->logs[1] = 0;

        for (int i {2}; i <= n; ++i) {
            this->logs[i] = this->logs[i / 2] + 1;
        }

        this->arr.assign(n, vector<T>(this->logs[n] + 1));

        for (int i {}; i < n; ++i) {
            this->arr[i][0] = v[i];
        }

        for (int k {1}; (1 << k) <= n; ++k) {
            for (int i {}; i + (1 << k) - 1 < n; ++i) {
                this->arr[i][k] = this->fn(this->arr[i][k - 1], this->arr[i + (1 << (k - 1))][k - 1]);
            }
        }
    }
};
```

---