```ad-info
title: Objetivo

- Encontrar o fecho convexo, ou seja, o menor polígono convexo tal que ele contenha todos os pontos. A implementação utiliza o [[Point2D]] e as suas funções clockwise, counterclockwise e orientation.
```

```ad-note
title: Complexidade
collapse: true

- $O(n \log n)$
```

```cpp
template <typename T>
vector<Point2D<T>> monotone_chain(vector<Point2D<T>> &points, bool include_collinear = false) {
	sort(points.begin(), points.end());

	vector<Point2D<T>> up, down;

    Point2D<T> p1 {points[0]}, p2 {points.back()};

    up.push_back(p1);
    down.push_back(p1);

    for (int i {1}; i < points.size(); ++i) {
        if (i == points.size() - 1 || cw(p1, points[i], p2, include_collinear)) {
            while (up.size() >= 2 
                && !cw(up[up.size() - 2], up.back(), points[i], include_collinear)
            ) {
                up.pop_back();
            }

            up.push_back(points[i]);
        }

        if (i == points.size() - 1 || ccw(p1, points[i], p2, include_collinear)) {
            while (down.size() >= 2
                && !ccw(down[down.size() - 2], down.back(), points[i], include_collinear)
            ) {
                down.pop_back();
            }

            down.push_back(points[i]);
        }
    }

	if (include_collinear && up.size() == points.size()) {
		return reverse(up.begin(), up.end());
	}

	vector<Point2D<T>> convex_hull {move(up)};

	for (int i {int(down.size() - 2)}; i > 0; --i) {
		convex_hull.push_back(down[i]);
	}

	return convex_hull;
}
```

---