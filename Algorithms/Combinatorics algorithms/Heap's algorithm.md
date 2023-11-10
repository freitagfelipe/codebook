> [!info] Objetivo
> - Tem como objetivo calcular todas as permutações desse conjunto.

> [!note]- Complexidade
> - $O(n \cdot n!)$

```cpp
template <typename T>
void heap_permutation(vector<T> &v, int size) {
    if (size == 1) {
	    // Do something with the permutation

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