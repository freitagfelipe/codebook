> [!info] Objetivo
> Encontrar em um vetor ordenado um elemento que tenha alguma propriedade tal que com essa propriedade seja possível descrever três coisas: se o elemento foi encontrado, se o elemento procurado é menor que o atual ou se o elemento procurado é maior do que o atual.

> [!caution] Restrição
> O vetor deve estar ordenado em ordem crescente.

> [!faq] Como funciona?
> Dado que o vetor está ordenado e a propriedade consiga me responder se o elemento procurado é menor que o atual, se o elemento procurado é maior que o atual ou se o elemento procurado é o atual, a busca binária irá escolher o elemento do meio do vetor e checará a propriedade, se ela nos retornar que o elemento procurado é menor que o atual basta descartar todos os elementos do meio até o fim, caso contrário se ela nos retornar que o elemento procurado é maior que o atual basta descartar todos os elementos do meio até o começo. Portanto, basta repetir esses passos até que o elemento seja encontrado ou não.

> [!note]- Complexidade
> $O(\log n)$, que é o tamanho máximo da árvore de recursão.

`````ad-example
title: Procurar um elemento $x$ no vetor.

```cpp
bool binary_search(const vector<int> &v, int x) {
    int start {}, end {v.size() - 1};

    while (start <= end) {
        int mid {(start + end) / 2};

        if (v[mid] == x) {
            return true;
        } else if (v[mid] > x) {
            end = mid - 1;
        } else {
            start = mid + 1;
        }
    }

    return false;
}
```
`````

---