> [!info] Objetivo
> - Encontrar a maior subsequência comum entre dois vetores.

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

> [!hint] Retornar a maior subsequência comum
> - O código abaixo pode ser utilizado para retornar a LCS.

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

> [!hint] Encontrar a LCS utilizando uma LIS
> - Caso uma das sequências tenha apenas elementos distintos a LCS pode ser calculada por meio de uma [[Longest increasing subsequence (LIS)]] como mostrado abaixo.

````ad-example
title: Exemplo com a questão [Não é só mais um LCS](https://neps.academy/br/exercise/301).

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
#include <bits/stdc++.h>

using namespace std;

unordered_map<int, int> mp;

int main() {
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	
    int n, m;

    cin >> n >> m;

    for (int i {}; i < n; ++i) {
        int aux;

        cin >> aux;
		
		mp[aux] = i;
    }

    vector<int> lis;

    for (int i {}; i < m; ++i) {
        int aux;

        cin >> aux;

        if (mp.find(aux) == mp.end()) {
            continue;
        }

        vector<int>::iterator it {lower_bound(lis.begin(), lis.end(), mp[aux])};

        if (it == lis.end()) {
            lis.push_back(mp[aux]);
        } else {
            *it = mp[aux];
        }
    }

    cout << lis.size() << '\n';

    return 0;
}
```
````

---