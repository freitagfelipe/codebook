```cpp
// Consegue calcular a distância de um ponto p até uma reta r descrita pelos pontos a e b.
template <typename T>
double distance_between_line_and_point(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &p) {
	Point2D<T> ab {b - a}, ap {p - a};

	T distance {abs(cross(ap, ab))};

	return distance / distance_between_points(a, b);
}
```

---