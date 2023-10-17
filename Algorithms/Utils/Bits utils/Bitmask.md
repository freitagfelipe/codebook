> [!info] Objetivo
> - Uma máscara de bits é a representação de um subconjunto feita a partir da representação binária de um número. Os métodos a seguir podem ser utilizados nela.

> [!note]- Complexidade
> - Is submask, intersection, merge, complement: $O(1)$
> - Iterate through submasks: $O(2^n)$

```cpp
bool is_submask(int a, int b) {
    return (a & b) == b;
}
```

```cpp
int intersection(int a, int b) {
    return a & b;
}
```

```cpp
int merge(int a, int b) {
    return a | b;
}
```

```cpp
int complement(int a) {
    return ~a;
}
```

```cpp
void iterate_through_submasks(int x) {
    for (int i {x}; i > 0; i = (i - 1) & x) {
        // do something
    }
}
```

---