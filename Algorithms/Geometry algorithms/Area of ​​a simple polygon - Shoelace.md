> [!info] Objetivo
> - Tem como objetivo calcular a área desse polígono. Ademais, a implementação utiliza o [[Point2D]] e para calcular a área ele utiliza a fórmula de Shoelace que é dada por:
> $$
> \begin{gathered}
> A = \dfrac{1}{2} \cdot |\sum_{i = 1}^{n} (y_{i + 1} + y_i) \cdot (x_{i + 1} - x_i)|
> \end{gathered}
> $$

> [!caution] Atenção
> - A implementação só funcionará se os pontos estiverem no sentido horário ou anti-horário.

> [!note]- Complexidade
> - $O(n)$

```cpp
template <typename T>
double calculate_area(const vector<Point2D<T>> &polygon) {
	T ans {};

	for (int i {}; i < (int) polygon.size(); ++i) {
		Point2D<T> q {i ? polygon[i - 1] : polygon.back()};
		Point2D<T> p {polygon[i]};

		ans += (p.y + q.y) * (p.x - q.x);
	}

	return abs(ans) / 2; // use fabs in cases where T is double or float
}
```

```cpp
template <typename T>
T calculate_two_times_area(const vector<Point2D<T>> &polygon) {
	T ans {};

	for (int i {}; i < (int) polygon.size(); ++i) {
		Point2D<T> q {i ? polygon[i - 1] : polygon.back()};
		Point2D<T> p {polygon[i]};

		ans += (p.y + q.y) * (p.x - q.x);
	}

	return abs(ans); // use fabs in cases where T is double or float
}
```

---