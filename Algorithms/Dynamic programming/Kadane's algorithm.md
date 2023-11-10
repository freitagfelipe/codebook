> [!info] Objetivo
> - Tem como objetivo calcular a soma máxima daquele conjunto, ou seja, encontrar a subsequência contínua de $v$ que tenha a maior soma.

> [!note]- Complexidade
> - $O(n)$

```cpp
int kadane(const vector<int> &v) {
    int sum {v[0]};
    int ans {v[0]};

    for (int i {1}; i < (int) v.size(); ++i) {
        sum = max(v[i], sum + v[i]);
        ans = max(ans, sum);
    }

    return ans;
}
```

> [!hint] Encontrando o início e o fim da subsequência
> - O algoritmo de Kadane pode ser adaptado para encontrar o início e o fim da subsequência contínua de soma máxima com a mesma complexidade.

```cpp
typedef pair<int, int> pii;

pii kadane(const vector<int> &v) {
	vector<int> DP(v.size()), opt(v.size());

    DP[0] = v[0];
    opt[0] = 0;
    
    for (int i {1}; i < (int) v.size(); ++i) {
        if (v[i] >= v[i] + DP[i - 1]) {
            opt[i] = i;
        } else {
            opt[i] = opt[i - 1];
        }
    
        DP[i] = max(v[i], DP[i - 1] + v[i]);
    }

    int answer {DP[0]}, optimal {};
    
    for (int i {1}; i < (int) v.size(); ++i) {
        if (answer < DP[i]) {
            answer = DP[i];
            optimal = i;
        }
    }

    return {opt[optimal], optimal};
}
```

> [!hint] Vetor circular
> - O algoritmo de Kadane pode ser adaptado para encontrar a subsequência de $v$ que tem a maior soma tal que $v$ é um vetor circular.

```cpp
int circular_kadane(vector<int> &v) {
    int all {v[0]};
    int ans {v[0]}, sum {v[0]};
    int inverse_ans {v[0] * -1}, inverse_sum {v[0] * -1};

    for (int i {1}; i < (int) v.size(); ++i) {
        inverse_sum = max(v[i] * -1, inverse_sum + v[i] * -1);
        inverse_ans = max(inverse_ans, inverse_sum);

        sum = max(v[i], sum + v[i]);
        ans = max(ans, sum);

        all += v[i];
    }

    return max(ans, all + inverse_ans);
}
```

---