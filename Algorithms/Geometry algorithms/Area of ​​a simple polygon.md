```ad-info
title: Objetivo

- Calcular a área de um polígono simples e cíclico, ou seja, os segmentos consecutivos que o formam não são colineares, não se cruzam e se tocam apenas nas extremidades e existe uma circunferência que intercepta seus vértices. A implementação utiliza o [[Point2D]] e utiliza a Shoelace formula utilizando trapézios, que é dada por:

$$
\begin{gathered}
A = \dfrac{1}{2} \cdot |\sum_{i = 1}^{n} (y_{i + 1} + y_i) \cdot (x_{i + 1} - x_i)|
\end{gathered}
$$
```

```ad-attention
title: Atenção

- A implementação só funcionará se os pontos estiverem em ordem horária ou anti-horária.
```

```ad-note
title: Complexidade
collapse: false

- $O(n)$
```

```cpp
template <typename T>
double calculate_area(vector<Point2D<T>> polygon) {
	polygon.push_back(polygon[0]);

	double ans {};

	for (int i {}; i < polygon.size() - 1; ++i) {
		int sum_y {polygon[i + 1].y + polygon[i].y};
		int diff_x {polygon[i + 1].x - polygon[i].x};

		ans += diff_x * sum_y;
	}

	return abs(ans / 2);
}
```

---