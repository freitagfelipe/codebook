> [!info] Objetivo
> - Gerar todas as permutações de um conjunto.

> [!note]- Complexidade
> - $O(n \cdot n!)$

```cpp
ostream &operator<<(ostream &os, const vector<int> &v) {
	int c {};

	for (int n : v) {
		if (c++ > 0) {
			os << " ";
		}

		os << n;
	}

	return os;
}

void heap_permutation(vector<int> &v, int size) {
    if (size == 1) {
        cout << v << '\n';

        return;
    }
 
    for (int i {}; i < size; i++) {
        heap_permutation(v, size - 1);
 
        if (size % 2 == 1) {
            swap(v[0], v[size - 1]);
        } else {
            swap(v[i], v[size - 1]);
        }
    }
}
```

---