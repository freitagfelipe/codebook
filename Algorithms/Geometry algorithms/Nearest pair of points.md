> [!info] Objetivo
> - Dado um conjunto de pontos, o problema é encontrar o par de pontos como menor distância dentre todos os outros. Esta implementação utiliza [[Line sweep]] e do fato que temos um número constante de pontos ativos durante o processamento dos eventos. Ademais, a implementação utiliza o [[Point2D]] e sua função [[Distance between points]].

> [!caution] Restrição
> - Os pontos devem estar ordenados pelo menor $x$.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
template <typename T>
using ptt = pair<T, T>;

template <typename T>
double find_minimum_distance(vector<Point2D<T>> points) {
	int n {(int) points.size()};

	// Sort them according to their x-coordinates in ascending order
	sort(points.begin(), points.end());

	int fp {};
	set<ptt<T>> active_points;

	double ans {distance_between_points(points[0], points[1])};

	for (int i {}; i < n; ++i) {
		while (fp < i && points[i].x - points[fp].x >= ans) {
			active_points.erase({points[fp].y, fp});

			++fp;
		}

		auto it {active_points.lower_bound({points[i].y - ans, 0})};

		while (it != active_points.end() && it->first < points[i].y + ans) {
			ans = min(ans, distance_between_points(points[i], points[it->second]));
			
			++it;
		}

		active_points.insert({points[i].y, i});
	}

	return ans;
}
```

---