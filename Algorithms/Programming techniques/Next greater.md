> [!info] Objetivo
> - A técnica tem como objetivo dado um vetor, calcular para cada $v_i$ o maior elemento após ele. Por se tratar de uma técnica é necessário adaptar dependendo da questão.

> [!note]- Complexidade
> - $O(n)$

```cpp
typedef pair<int, int> pii;

vector<pii> next_greater(const vector<int> &v) {
    vector<pii> nge(v.size(), {-1, -1});
    stack<int> s;

    s.push(0);

    for (int i {1}; i < (int) v.size(); ++i) {
        if (v[i] <= v[s.top()]) {
            s.push(i);

            continue;
        }

        while (!s.empty() && v[i] > v[s.top()]) {
            nge[s.top()] = {v[i], i};

            s.pop();
        }
    }

    return nge;
}
```

---

