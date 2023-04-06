```ad-info
title: Objetivo

- A técnica de dois ponteiros pode ser usada de várias maneiras, mas sua utilização sempre consiste em usar dois ponteiros para apontar para lugares de um vetor. Por se tratar de uma técnica é necessário adaptá-la de acordo com as necessidades.
```

```ad-note
title: Complexidade
collapse: true

- $O(N)$
```

`````ad-example
title: Encontrar dois números que somam $K$.

```ad-attention
title: Restrição

- A entrada tem que estar ordenada.
```

```cpp
#include <iostream>

using namespace std;

#define MAXN 100001

int h[MAXN];

int main() {
    int n, k;

    cin >> n;

    for (int i {}; i < n; ++i) {
        cin >> h[i];
    }

    cin >> k;

    int i {}, j {n - 1};

    while (i <= j) {
        if (h[i] + h[j] == k) {
            break;
        } else if (h[i] + h[j] > k) {
            --j;
        } else {
            ++i;
        }
    }

    cout << h[i] << " " << h[j] << '\n';

    return 0;
}
```
`````

````ad-example
title: Encontrar quantos intervalos em um vetor somam $K$

```ad-attention
title: Restrição

- Para o exemplo abaixo a entrada tem que conter apenas números maiores que um, pois caso contrário para um mesmo $p2$ existiriam vários $p1$, e não precisa seguir a restrição anterior. Caso aconteça de ter números menores ou iguais a zero podemos utilizar uma adaptação da técnica de [[Prefix sum array (PSA)]] ou [[Tree pointers]], mas caso tenha números negativos a técnica de três ponteiros não funciona.
```

```cpp
#include <bits/stdc++.h>

using namespace std;

#define MAXN 100001

int v[MAXN];

int main() {
    int n, k;
    
    cin >> n >> k;
    
    for (int i {}; i < n; ++i) {
        cin >> v[i];
    }
    
    int p1 {}, p2 {}, sum {v[0]}, answer {};
    
    while (p1 < n && p2 < n) {
        if (sum == k) {
            ++answer;
        }
        
        if (sum <= k) {
            if (++p2 < n) {
                sum += v[p2];
            }
        } else {
            sum -= v[p1++];
        }
    }
    
    cout << answer << '\n';

    return 0;
}
```
````

---