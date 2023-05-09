```ad-info
title: Objetivo

- Dado um conjunto de pontos, o problema é encontrar o par de pontos como menor distância dentre todos os outros. Esta implementação utiliza line sweep e do fato que temos um número constante de pontos ativos durante o processamento dos eventos. Ademais, a implementação utiliza o [[Point2D]] e sua função de distância entre pontos.
```

```ad-note
title: Complexidade
collapse: true

- $O(n \log n)$
```

```cpp
typedef pair<int, int> pii;

template <typename T>
double find_minimum_distance(vector<Point2D<T>> points) {
	sort(points.begin(), points.end());

	int first_active_point {};
	set<pii> active_points;

	double answer {distance_between_points(points[0], points[1])};

	for (int i {}; i < points.size(); ++i) {
		while (points[i].x - points[first_active_point].x > answer) {
			active_points.erase({points[first_active_point].y, first_active_point});

			++first_active_point;
		}

		pii search_point {points[i].y - answer, 0};
		set<pii>::iterator it {active_points.lower_bound(search_point)};

		while (it != active_points.end() && it->first <= points[i].y + answer) {
			answer = min(answer, distance_between_points(points[i], points[it->second]));

			++it;
		}

		active_points.insert({points[i].y, i});
	}

	return answer;
}
```

---