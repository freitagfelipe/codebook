> [!info] Objetivo
> - A implementação abaixo do algoritmo tem como objetivo ordenar o vetor em ordem crescente.

>[!note]- Complexidade
>- $O(n \log n)$

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