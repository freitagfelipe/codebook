> [!info] Objetivo
> - Calcular a projeção do vetor $\vec{a}$ em relação ao vetor $\vec{b}$ utilizando [[Point3D]] e suas funções [[Algorithms/Utils/Geometry utils/Point3D/Dot product|Dot product]] e [[Algorithms/Utils/Geometry utils/Point3D/Length|Length]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
double projection(const Point3D<T> &a, const Point3D<T> &b) {
	return dot(a, b) / length(b);
}
```

---