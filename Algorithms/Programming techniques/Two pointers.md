> [!info] Objetivo
> A técnica de dois ponteiros pode ser usada de algumas maneiras por se tratar de uma técnica, mas sua utilização sempre consiste em usar dois ponteiros para apontar para lugares de um vetor.

> [!note]- Complexidade
> $O(n)$ 

`````ad-example
title: Encontrar dois números que somam $K$ em um vetor.

> [!caution] Restrição
> O vetor deve estar ordenado em ordem crescente.

> [!faq] Como funciona?
> Nessa adaptação como o vetor está ordenado, nos colocaremos um ponteiro no início e outro no fim, caso a soma dos elementos seja maior que o elemento procurado basta mover o ponteiro do fim para a esquerda e com isso diminuiremos a soma, caso o elemento procurado seja maior que a soma dos elementos basta mover o ponteiro do início para a dereita e com isso aumentaremos a soma, repetiremos esse processo até encontrar o elemento ou até que os ponteiros se encontrem, nesse caso o vetor não possui dois elementos que somem $k$.

```cpp
#include <bits/stdc++.h>

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

    while (i < j) {
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

> [!caution] Restrição
> Para o exemplo abaixo a entrada tem que conter apenas números maiores ou iguais a um, pois caso contrário para um mesmo $p2$ existiriam vários $p1$, e não precisa seguir a restrição anterior. Caso aconteça de ter números iguais a zero podemos utilizar uma adaptação da técnica de [[Prefix sum array (PSA)]] ou [[Tree pointers]], mas caso tenha números negativos a técnica de três ponteiros não funcionará.

> [!faq] Como funciona?
> Começaremos ambos os ponteiros no início do vetor e armazenaremos uma variável com a soma dos elementos de $p1$ até $p2$, caso a soma desses elementos seja menor ou igual a $K$ basta deslocar $p2$ uma unidade para a direita e adicionemos esse elemento na soma, caso a soma dos elementos seja maior que $K$ basta deslocar $p1$ uma casa para a direita e diminuir o antigo elemento que $p1$ apontava da soma e antes de cada um desses passos basta checarmos se a soma desse intervalo formado pelos elementos de $p1$ até $p2$ somam $K$.

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