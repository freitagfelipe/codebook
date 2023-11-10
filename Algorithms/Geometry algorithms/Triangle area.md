> [!info] Objetivo
> - Tem como objetivo calcular a área de um triângulo utilizando a implementação do [[Point2D]] e utilizando sua função de [[Algorithms/Utils/Geometry utils/Point2D/Cross product|Cross product]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
T triangle_area(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
	return abs(cross(b - a, c - a)) / 2; // use fabs in cases where T is double
}
```

---

> [!info] Objetivo
> - Tem como objetivo calcular a área de um triângulo utilizando a fórmula de Heron.

> [!note]- Complexidade
> - $O(1)$

```cpp
double triangle_area(double a, double b, double c) {
	double p {(a + b + c) / 2};

	return sqrt(p * (p - a) * (p - b) * (p - c));
}
```

---