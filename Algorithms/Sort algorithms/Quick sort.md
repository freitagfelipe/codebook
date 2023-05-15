> [!info] Objetivo
> A implementação abaixo do algoritmo tem como objetivo ordenar o vetor em ordem crescente.

> [!faq] Como funciona?
> O algoritmo de quick sort funciona utilizando divisão e conquista, o primeiro passo do algoritmo é fazer com que um elemento, chamado de pivô fique em uma posição do vetor tal que todos os elementos a sua esquerda sejam menores ou iguais a ele e os da direita sejam estritamente maiores que ele, feito isso, ele irá chamar recursivamente a função para a esquerda do pivô e para a direita enquanto o tamanho do vetor para aquela instância seja maior que dois, ao término dessas chamadas o vetor estará ordenado. As pré-condições para utilizar o algoritmo abaixo é que $start = 0$ e $end = |v| - 1$.

>[!note]- Complexidade
>$O(n \log n)$

```cpp
int partition(vector<int> &v, int start, int end) {
	int i {start + 1}, j {end};
	int pivot {v[start]};

	while (i <= j) {
		if (v[i] <= pivot) {
			++i;
		} else if (v[j] > pivot) {
			--j;
		} else {
			swap(v[i++], v[j++]);
		}
	}

	swap(v[start], v[j]);

	return j;
}

void quick_sort(vector<int> &v, int start, int end) {
	if (start < end) {
		int pi {partition(v, start, end)};

		quick_sort(v, start, pi - 1);
		quick_sort(v, pi + 1, end);
	}
}
```

---