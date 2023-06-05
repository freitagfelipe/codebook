> [!info] Objetivo
> - Calcular a distância entre os pontos $a$ e $b$ utilizando a fórmula da distância euclidiana.

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
double distance_between_points(const Point2D<T> &a, const Point2D<T> &b) {
	T dx {a.x - b.x};
	T dy {a.y - b.y};

	return sqrt(dx * dx + dy * dy);
}
```

---