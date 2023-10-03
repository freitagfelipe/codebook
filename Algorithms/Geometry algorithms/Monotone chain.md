> [!info] Objetivo
> - Encontrar o fecho convexo, ou seja, o menor polígono convexo tal que ele contenha todos os pontos. A implementação utiliza o [[Point2D]] e as suas funções [[Clockwise]], [[Counter clockwise]] e [[Collinear]].

> [!caution] Restrição
> - É necessário que os pontos estejam ordenados o menor para o maior $x$ e em caso de empate desempataremos pelo menor $y$.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
template <typename T>
vector<Point2D<T>> monotone_chain(vector<Point2D<T>> &points, bool include_collinear = false) {
	if (points.size() == 1) {
		return points;
	}

	// Sort them according to their x-coordinates in ascending order
	// In case of a tie, we will break the tie by the lowest y
	sort(points.begin(), points.end());

    int n {(int) points.size()};
    Point2D<T> p1 {points[0]}, p2 {points.back()};

    // This treat the case where all the input points are collinear and return the input
    // In reverse order, that would be what Graham's Scan algorithm would return
	for (int i {1}; i < n - 1; ++i) {
        if (!collinear(p1, points[i], p2)) {
            break;
        }

        if (i + 1 == n - 1) {
            vector<Point2D<T>> hull {points};

            reverse(hull.begin(), hull.end());

            return hull;
        }
	}

	vector<Point2D<T>> up, down;

    up.push_back(p1);
    down.push_back(p1);

    for (int i {1}; i < n; ++i) {
        if (i == n - 1 || cw(p1, points[i], p2, include_collinear)) {
            while (up.size() >= 2 
                && !cw(up[up.size() - 2], up.back(), points[i], include_collinear)
            ) {
                up.pop_back();
            }

            up.push_back(points[i]);
        }

        if (i == n - 1 || ccw(p1, points[i], p2, include_collinear)) {
            while (down.size() >= 2
                && !ccw(down[down.size() - 2], down.back(), points[i], include_collinear)
            ) {
                down.pop_back();
            }

            down.push_back(points[i]);
        }
    }

	vector<Point2D<T>> convex_hull {up};

	for (int i {(int) down.size() - 2}; i > 0; --i) {
		convex_hull.push_back(down[i]);
	}

	return convex_hull;
}
```

---