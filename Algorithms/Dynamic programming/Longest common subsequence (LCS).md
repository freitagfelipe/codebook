> [!info] Objetivo
> - Tem como objetivo encontrar a maior subsequência comum entre $a$ e $b$.

> [!note]- Complexidade
> - $O(nm)$

```cpp
int lcs(const string &a, const string &b) {
    vector<vector<int>> tab(a.size() + 1, vector<int>(b.size() + 1));

    for (int i {}; i < (int) a.size(); ++i) {
        for (int j {}; j < (int) b.size(); ++j) {
            if (a[i] != b[j]) {
                tab[i + 1][j + 1] = max(tab[i + 1][j], tab[i][j + 1]);
            } else {
                tab[i + 1][j + 1] = tab[i][j] + 1;
            }
        }
    }

    return tab[a.size()][b.size()];
}
```

> [!hint] Encontrando a maior subsequência comum
> - O código abaixo pode ser utilizado para dizer qual é a maior subsequência comum entre $a$ e $b$.

```cpp
string lcs(const string &a, const string &b) {
	vector<vector<int>> tab(a.size() + 1, vector<int>(b.size() + 1));

    for (int i {}; i < (int) a.size(); ++i) {
        for (int j {}; j < (int) b.size(); ++j) {
            if (a[i] != b[j]) {
                tab[i + 1][j + 1] = max(tab[i + 1][j], tab[i][j + 1]);
            } else {
                tab[i + 1][j + 1] = tab[i][j] + 1;
            }
        }
    }

	int i {int(a.size() + 1)}, j {int(b.size() + 1)};
	string answer;

	while (i && j) {
		if (a[i - 1] == b[j - 1]) {
			answer.push_back(a[i - 1]);

			--i;
			--j;
		} else if (tab[i][j - 1] > tab[i - 1][j]) {
			--j;
		} else {
			--i;
		}
	}

	reverse(answer.begin(), answer.end());

	return answer;
}
```

---