```ad-info
title: Objetivo

- O primeiro algoritmo tem como objetivo utilizar a área de um triângulo utilizando a implementação do [[Point2D]] e utilizando sua função de cross product, já o segundo utiliza a fórmula de Heron.
```

```ad-note
title: Complexidade
collapse: true

- Ambos $O(1)$
```

```cpp
template <typename T>
T triangle_area(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
	return abs(cross(b - a, c - a)) / 2; // or fabs(cross(b - a, c - a)) / 2;
}
```

```cpp
double triangle_area(double a, double b, double c) {
	double p {(a + b + c) / 2};

	return sqrt(p * (p - a) * (p - b) * (p - c));
}
```

---