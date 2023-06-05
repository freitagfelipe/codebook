> [!info] Objetivo
> - A técnica de soma de prefixo é uma técnica que pode ser adaptada de várias maneiras.

````ad-example
title: Dado um vetor responder várias perguntas sobre qual é a soma do intervalo $[L, R]$.

> [!hint] Alterações no vetor
> Caso seja necessário fazer alterações no vetor além de dizer qual a soma do intervalo, vale a pena olhar a [[Fenwick tree (Binary Indexed Tree)]].

> [!note]- Complexidade
> - Build: $O(n)$
> - Query: $O(1)$

```cpp
#include <bits/stdc++.h>

using namespace std;

// MAXN is the maximum size of the array
#define MAXN 100001

int v[MAXN];
int psa[MAXN];

int main() {
    int n, q;

    cin >> n >> q;

    for (int i {}; i < n; ++i) {
        cin >> v[i];
    }

    psa[0] = v[0]

    for (int i {1}; i < n; ++i) {
        psa[i] = v[i] + psa[i - 1];
    }

    for (int i {}; i < q; ++i) {
        int l, r;

        cin >> l >> r;

        if (l == 0) {
            cout << psa[r] << '\n';
        } else {
            cout << psa[r] - psa[l - 1] << '\n';
        }
    }

    return 0;
}
```
````

````ad-example
title: Dado um vetor responder quantos intervalos de $V$ somam $K$.

> [!note]- Complexidade
> - $O(n)$

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;

int main() {
    int n, k;

    cin >> n >> k;

    unordered_map<ll, ll> freq;
    ll sum {}, ans {};

    freq[0] = 1;

    for (int i {}; i < n; ++i) {
        int v;

        cin >> v;

        sum += v;

        ans += freq[sum - k];

        ++freq[sum];
    }

    cout << ans << '\n';

    return 0;
}
```
````

---