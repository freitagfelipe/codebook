> [!info] Objetivo
> - Calcular a projeção do vetor $\vec{a}$ em relação ao vetor $\vec{b}$ utilizando [[Point2D]] e suas funções [[Algorithms/Utils/Geometry utils/Point2D/Dot product|Dot product]] e [[Algorithms/Utils/Geometry utils/Point2D/Length|Length]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
double projection(const Point2D<T> &a, const Point2D<T> &b) {
	return dot(a, b) / length(b);
}
```

---