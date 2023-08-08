> [!info] Objetivo
> - A técnica de soma de prefixo é uma técnica que pode ser adaptada de várias maneiras. Uma adaptação pode ser vista logo abaixo.

> [!note]- Complexidade

`````ad-example
title: Exemplo com a questão [Calculando Somas I](https://neps.academy/br/exercise/1876).

> [!note]- Complexidade
> - Build: $O(nm)$
> - Query: $O(1)$

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;

#define MAXN int(1e3) + 10

ll PSM[MAXN][MAXN];

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n, q;

    cin >> n >> q;

    for (int i {1}; i <= n; ++i) {
        for (int j {1}; j <= n; ++j) {
            int x;

            cin >> x;   

            PSM[i][j] = PSM[i - 1][j] + PSM[i][j - 1] - PSM[i - 1][j - 1] + x;
        }
    }

    while (q--) {
        int xi, yi, xe, ye;

        cin >> xi >> yi >> xe >> ye;

        cout << PSM[xe][ye] - PSM[xi - 1][ye] - PSM[xe][yi - 1] + PSM[xi - 1][yi - 1] << '\n';
    }

    return 0;
}
```
`````

---