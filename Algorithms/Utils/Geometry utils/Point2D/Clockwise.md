> [!info] Objetivo
> - Dizer se um vetor $\vec{c}$ centrado no ponto $a$ está no sentido horário do vetor $\vec{b}$ centrado em $a$ utilizando [[Point2D]] e sua função [[Orientation]]. Ademais, pode ser informado se é obrigatório considerar que um vetor colinear está no sentido horário.

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
bool cw(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, bool include_collinear = false) {
    int result {orientation(a, b, c)};

    return result < 0 || (include_collinear && result == 0);
}
```

---