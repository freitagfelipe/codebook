> [!info] Objetivo
> - Calcular o ângulo entre os vetores $\vec{a}$ e $\vec{b}$ utilizando [[Point3D]] e suas funções [[Algorithms/Utils/Geometry utils/Point3D/Dot product|Dot product]] e [[Algorithms/Utils/Geometry utils/Point3D/Length|Length]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
double angle(const Point3D<T> &a, const Point3D<T> &b) {
	return acos(dot(a, b) / length(a) / length(b));
}
```

---