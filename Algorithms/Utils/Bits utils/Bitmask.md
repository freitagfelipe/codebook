> [!note] Objetivo
> - Uma máscara de bits é a representação de um subconjunto feita a partir da representação binária de um número. Os métodos a seguir podem ser utilizados nela. A primeira função checa se $b$ é uma submáscara de $a$, a segunda função itera por todas as submáscaras de uma máscara.

```cpp
bool is_submask(int a, int b) {
    return (a & b) == b;
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