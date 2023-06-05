> [!info] Objetivo
> - Dizer se um vetor $\vec{c}$ centrado no ponto $a$ está no sentido anti-horário do vetor $\vec{b}$ centrado no ponto $a$ utilizando [[Point2D]] e sua função [[Orientation]]. Ademais, pode ser informado se é obrigatório considerar que um vetor colinear está no sentido anti-horário.

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
bool ccw(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, bool include_collinear = false) {
    int result {orientation(a, b, c)};

	return result > 0 || (include_collinear && result == 0);
}
```

---