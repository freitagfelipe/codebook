> [!info] Objetivo
> - Se parece muito com a técnica de [[Line sweep]], porém ao invés de termos uma linha se movendo pelo eixo $x$ ou pelo eixo $y$, temos uma semirreta centrada na origem do plano sendo rotacionada no sentido horário ou anti-horário. Ademais, a implementação deste algoritmo utiliza o [[Point2D]] e suas funções [[Algorithms/Utils/Geometry utils/Point2D/Cross product|Cross product]] e [[Algorithms/Utils/Geometry utils/Point2D/Norm|Norm]]. O código apresentado mostra apenas como ordenar os eventos.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
template <typename T>
int region_value(const Point2D<T> &a) {
	if (a.y > 0 || (a.y == 0 && a.x > 0)) {
		return 0;
	}

	return 1;
}

template <typename T>
bool cmp(const Point2D<T> &a, const Point2D<T> &b) {
	int a_region_value {region_value(a)};
	int b_region_value {region_value(b)}

	if (a_region_value != b_region_value) {
		return a_region_value < b_region_value;
	}

	T cross_result {cross(a, b)};

	if (cross_result != 0) {
		return cross_result > 0;
	}

	return norm(a) < norm(b);
}
```

---