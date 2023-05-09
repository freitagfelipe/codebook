```ad-info
title: Objetivo

- Resolver o problema da soma máxima de um intervalo, ou seja, dado um conjunto $S$ encontrar qual subsequência de $S$ tem a maior soma.
```

```ad-note
title: Complexidade
collapse: true

- $O(n)$
```

```cpp
int kadane(vector<int> &v) {
    int sum {v[0]};
    int ans {v[0]};

    for (int i {1}; i < v.size(); ++i) {
        sum = max(v[i], sum + v[i]);
        ans = max(ans, sum);
    }

    return ans;
}
```

```ad-hint
title: Adaptação

- Pode ser adaptado para encontrar também o início e o fim da subsequência como mostrado logo abaixo.
```

```cpp
typedef pair<int, int> pii;

int DP[MAXN];
int opt[MAXN];

pii kadane(vector<int> &v) {
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