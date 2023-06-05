> [!note] Objetivo
> - Verificar se um ponto $c$ está no segmento formados pelos pontos $a$ e $b$ utilizando [[Point2D]] e [[Algorithms/Utils/Geometry utils/Point2D/Cross product|Cross product]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
bool point_in_segment(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
	if (cross(b - a, c - a) != 0) {
		return false;
	}

	if (min(a.x, b.x) > c.x || c.x > max(a.x, b.x)) {
		return false;
	} else if (min(a.y, b.y) > c.y || c.y > max(a.y, b.y)) {
		return false;
	}

	return true;
}
```

---