```cpp
// Consegue calcular a distância de um ponto p até um segmento de reta r descrito pelos pontos a e b.
template <typename T>
double distance_between_segment_and_point(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &p) {
	if (dot(p - a, b - a) < 0) {
		return distance_between_points(p, a);
	} else if (dot(p - b, a - b) < 0) {
		return distance_between_points(p, b);
	}

	return distance_between_line_and_point(a, b, p);
}
```

---