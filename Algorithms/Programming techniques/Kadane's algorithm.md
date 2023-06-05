> [!info] Objetivo
> Resolver o problema da soma máxima de um intervalo, ou seja, dado um vetor $v$ ele encontra uma subsequência de $v$ que tenha a maior soma.

> [!note]- Complexidade
> - $O(n)$

```cpp
int kadane(const vector<int> &v) {
    int sum {v[0]};
    int ans {v[0]};

    for (int i {1}; i < v.size(); ++i) {
        sum = max(v[i], sum + v[i]);
        ans = max(ans, sum);
    }

    return ans;
}
```

> [!hint] Adaptação
> O algoritmo de Kadane pode ser adaptado para encontrar o início e o fim da sequência como mostrado logo abaixo.

> [!note]- Complexidade
> $O(n)$

```cpp
typedef pair<int, int> pii;

// MAXN is the max size of v
int DP[MAXN];
int opt[MAXN];

pii kadane(const vector<int> &v) {
    DP[0] = v[0];
    opt[0] = 0;
    
    for (int i {1}; i < v.size(); ++i) {
        if (v[i] >= v[i] + DP[i - 1]) {
            opt[i] = i;
        } else {
            opt[i] = opt[i - 1];
        }
    
        DP[i] = max(v[i], DP[i - 1] + v[i]);
    }

    int answer {DP[0]}, optimal {};
    
    for (int i {1}; i < v.size(); ++i) {
        if (answer < DP[i]) {
            answer = DP[i];
            optimal = i;
        }
    }

    return {opt[optimal], optimal};
}
```

---