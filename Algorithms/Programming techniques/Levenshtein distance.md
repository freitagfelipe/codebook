> [!info]
> - Encontrar a distância de edição entre duas sequẽncias que faça com que os conjuntos fiquem iguais.

> [!note]- Complexidade
> - $O(nm)$

```cpp
int edit_distance(const string &a, const string &b) {
    vector<vector<int>> tab(a.size() + 1, vector<int>(b.size() + 1, 0));

    for (int i {}; i <= a.size(); ++i) {
        tab[i][0] = i;
    }

    for (int i {}; i <= b.size(); ++i) {
        tab[0][i] = i;
    }

    for (int i {}; i < a.size(); ++i) {
        for (int j {}; j < b.size(); ++j) {
            int cost {};

            if (a[i] != b[j]) {
                cost = 1;
            }

            tab[i + 1][j + 1] = min({tab[i][j] + cost, tab[i + 1][j] + 1, tab[i][j + 1] + 1});
        }
    }

    return tab[a.size()][b.size()];
}
```

---