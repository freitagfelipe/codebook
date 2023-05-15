> [!info] Objetivo
> A implementação abaixo do algoritmo tem como objetivo ordenar um vetor em ordem crescente.

> [!faq] Como funciona?
> O algoritmo de merge sorte funciona utilizando divisão e conquista para conseguir ordenar o vetor, primeiro ele o dividide até que tenha tamanho menor que dois que é o caso base dele, pois um vetor com um ou zero elementos já está ordenado, feito isso ele irá realizar a junção desses vetores de uma maneira em que a ordenação seja mantida, após todas as junções o vetor estará ordenado. As pré-condições para utilizar o algoritmo abaixo é que $start = 0$ e $end = |v| - 1$.

> [!note]- Complexidade
> $O(n \log n)$, $\log n$ que é o tamanho máximo da árvore de recursão e $n$ para o processo de merge dos vetores.

```cpp
void merge(vector<int> &v, int start, int end) {
    vector<int> result;

    int p1 {start}, mid {(start + end) / 2}, p2 {mid + 1};

    while (p1 <= mid && p2 <= end) {
        if (v[p1] <= v[p2]) {
            result.push_back(v[p1++]);
        } else {
            result.push_back(v[p2++]);
        }
    }

    while (p1 <= mid) {
        result.push_back(v[p1++]);
    }

    while (p2 <= end) {
        result.push_back(v[p2++]);
    }

    copy(result.begin(), result.end(), v.begin() + start);
}

void merge_sort(vector<int> &v, int start, int end) {
    if (end > start) {
        int mid {(start + end) / 2};

        merge_sort(v, start, mid);
        merge_sort(v, mid + 1, end);

        merge(v, start, end);
    }
}
```

---