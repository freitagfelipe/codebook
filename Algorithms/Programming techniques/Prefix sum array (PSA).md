> [!info] Objetivo
> A técnica de soma de prefixo é uma técnica que pode ser adaptada de várias maneiras.

````ad-example
title: Dado um vetor responder várias perguntas sobre qual é a soma do intervalo $[L, R]$.

> [!faq] Como funciona?
> O vetor $psa$ na posição $i$ irá guardar as somas dos elementos de $v[1..i]$. Por isso, quando um intervalo nos for dado basta dizermos que a soma é $psa[r] - psa[l - 1]$, porém quando $l$ for zero, devemos retornar apenas a soma de $psa[r]$. Isso funciona pois estamos fazendo basicamente $(v_1 + v_2 + \ldots v_r) - (v_1 + v_2 + \ldots v_{l - 1}) = (v_l + \ldots + v_r)$.

> [!hint] Alterações no vetor
> Caso seja necessário fazer alterações no vetor além de dizer qual a soma do intervalo, vale a pena olhar a [[Fenwick tree (Binary Indexed Tree)]].

> [!note]- Complexidade
> Build: $O(n)$, pois o laço para montar a $PSA$ é linear e só utiliza operações constantes.
> Query: $O(1)$, pois só precisamos fazer dois acessos ao vetor em tempo constante.

```cpp
#include <bits/stdc++.h>

using namespace std;

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

> [!faq] Como funciona?
> Queremos descobrir quantos intervalos somam $K$, ou seja, quantos $psa[r] - psa[l - 1] = K$. Portanto, fazendo algumas alterações na fórmula, basta descobrirmos quantos $psa[l - 1] = psa[r] - k$, com isso basta salvarmos a frequência com que cada soma acumulada ocorre. Logo de início a soma de valor zero ocorre que é um intervalo vazio, por isso, iniciaremos a frequência dela com um, agora para cada elemento da sequência somaremos ele na variável de $sum$ e checaremos quantas vezes $sum - k$ apareceu e incrementaremos isso a resposta, após isso devemos incrementar a frequência de $sum$ e ao final desse processo teremos a resposta.

> [!note]- Complexidade
> $O(n)$, pois o laço é linear e atualizar o hash map é constante.

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