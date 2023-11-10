> [!info] Objetivo
> - Tem como objetivo ordenar um conjunto de elementos em ordem crescente.

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

// 0-indexed
void quick_sort(vector<int> &v, int start, int end) {
	if (start < end) {
		int pi {partition(v, start, end)};

		quick_sort(v, start, pi - 1);
		quick_sort(v, pi + 1, end);
	}
}
```

---