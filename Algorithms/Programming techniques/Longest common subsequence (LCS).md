```ad-note
title: Complexidade
collapse: true

- $O(nm)$
```

```cpp
size_t LCS(string &a, string &b) {
    vector<vector<int>> tab(a.size() + 1, vector<int>(b.size() + 1, 0));

    for (int i {}; i < a.size(); ++i) {
        for (int j {}; j < b.size(); ++j) {
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

`````ad-hint
title: Caso uma das sequências tenha apenas elementos destintos

- Nesse caso a LCS pode ser feita por meio de uma [[Longest increasing subsequence (LIS)]] adaptada da seguinte maneira mostrada logo abaixo no exemplo. Com complexidade de uma [[Longest increasing subsequence (LIS)]].
``````

````ad-example
title: LIS para encontrar LCS.

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