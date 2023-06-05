> [!info] Objetivo
> - Calcular o ângulo entre os vetores $\vec{a}$ e $\vec{b}$ utilizando a definição de [[Point2D]] e suas funções [[Algorithms/Utils/Geometry utils/Point2D/Dot product|Dot product]] e [[Algorithms/Utils/Geometry utils/Point2D/Length|Length]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
double angle(const Point2D<T> &a, const Point2D<T> &b) {
	return acos(dot(a, b) / length(a) / length(b));
}
```

---