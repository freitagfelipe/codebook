> [!info] Objetivo
> - A técnica de três ponteiros pode ser usada de várias maneiras, mas sua utilização sempre consiste em usar três ponteiros para apontar para lugares de um vetor. Por se tratar de uma técnica é necessário adaptá-la de acordo com as necessidades.

`````ad-example
title: Exemplo com a questão [Soma](https://neps.academy/br/exercise/468) da OBI 2019 - primeira fase.

> [!caution] Restrição
> - O vetor não pode conter números negativos, apenas números maiores ou iguais a zero. Caso o vetor contenha números negativos é necessário utilizar [[Prefix sum array (PSA)]].

> [!note]- Complexidade
> - $O(n)$

```cpp
#include <bits/stdc++.h>
 
using namespace std;

typedef long long ll;

// MAXN is the maximum size of the array
#define MAXN 5 * int(1e5) + 10 

int v[MAXN];

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int n, k;

    cin >> n >> k;
    
    for(int i {1}; i <= n; i++) {
        cin >> v[i];
    }
    
    ll sum {}, sum1 {}, sum2 {}, ans {};
    int p1 {}, p2 {};
    
    for(int p3 {1}; p3 <= n; p3++) {
        sum += v[p3];

        ll need {sum - k};
        
        while(p1 + 1 <= p3 && sum1 < need) {
            sum1 += v[++p1];
        }

        while(p2 + 1 <= p3 && sum2 <= need) {
            sum2 += v[++p2];
        }

        ans += p2 - p1;
    }
    
    cout << ans << '\n';
    
    return 0;
}
```
`````

---