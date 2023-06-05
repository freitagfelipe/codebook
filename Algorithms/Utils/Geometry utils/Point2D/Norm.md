> [!info] Objetivo
> - Calcular o tamanho ao quadrado de um vetor $\vec{a}$ utilizando [[Point2D]] e [[Algorithms/Utils/Geometry utils/Point2D/Dot product|Dot product]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
T norm(const Point2D<T> &a) {
	return dot(a, a);
}
```

---

