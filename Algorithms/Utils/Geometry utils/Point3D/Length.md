> [!info] Objetivo
> - Calcular o tamanho de um vetor $\vec{a}$ utilizando [[Point3D]] e sua função [[Algorithms/Utils/Geometry utils/Point3D/Dot product|Dot product]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
double length(const Point3D<T> &a) {
	return sqrt(dot(a, a));
}
```

---