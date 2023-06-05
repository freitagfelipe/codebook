> [!info] Objetivo
> Encontrar em um vetor ordenado um elemento que tenha alguma propriedade tal que com essa propriedade seja possível descrever três coisas: se o elemento foi encontrado, se o elemento procurado é menor que o atual ou se o elemento procurado é maior do que o atual.

> [!caution] Restrição
> - O vetor deve estar ordenado em ordem crescente.

`````ad-example
title: Procurar um elemento $x$ no vetor.

> [!note]- Complexidade
> - $O(\log n)$

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