> [!info] Objetivo
> Encontrar em um vetor ordenado um elemento que tenha alguma propriedade tal que com essa propriedade seja possível descrever três coisas: se o elemento foi encontrado, se o elemento procurado é menor que o atual ou se o elemento procurado é maior do que o atual.

> [!caution] Restrição
> - O vetor deve estar ordenado em ordem não crescente nos exemplos mostrados abaixo.

`````ad-example
title: Procurar um elemento $x$ no vetor.

> [!note]- Complexidade
> - $O(\log n)$

```cpp
bool binary_search(const vector<int> &v, int x) {
    int start {}, end {(int) v.size() - 1};

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

`````ad-example
title: Encontrar o maior $i$, tal que $v[i] <= x$ e caso esse elemento não exista retornar $-1$

> [!note]- Complexidade
> - $O(\log n)$

```cpp
int binary_search(const vector<int> &v, int k) {
    int start {}, end {(int) v.size() - 1}, ans {-1};

    while (start <= end) {
        int mid {(start + end) / 2};

        if (v[mid] <= k) {
            ans = mid;

            start = mid + 1;
        } else {
            end = mid - 1;
        }
    }

	return ans;
}
```
`````

`````ad-example
title: Encontrar o menor $i$, tal que $v[i] >= x$ e caso esse elemento não exista retornar $n$.

> [!note]- Complexidade
> - $O(\log n)$

```cpp
int binary_search(vector<int> &v, int k) {
	int start {}, end {(int) v.size() - 1}, ans {-1};

    while (start <= end) {
        int mid {(start + end) / 2};

        if (v[mid] < k) {
            start = mid + 1;
        } else {
            ans = mid;

            end = mid - 1;
        }
    }

    return ans;
}
```
`````

---