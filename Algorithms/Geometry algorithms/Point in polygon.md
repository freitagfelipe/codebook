> [!info] Objetivo
> - Tem como objetivo descobrir se um ponto $t$ está dentro, fora ou em cima de uma aresta de um polígono convexo. Ademais, utiliza o [[Point2D]] e suas funções [[Clockwise]] e [[Point in segment]]

> [!caution] Restrição
> - O polígono precisa ser convexo.
> - Os pontos precisam estar ordenados em sentido horário.
> - O primeiro ponto deve ser o com menor $x$.

> [!note]- Complexidade
> - $O(\log n)$

```cpp
template <typename T>
int get_region(const vector<Point2D<T>> &points, const Point2D<T> &t) {
    if (!cw(points[0], points[1], t)) {
        return 0;
    }
 
    if (!cw(points.back(), points[0], t)) {
        return 0;
    }
 
	int start {1}, end {(int) points.size() - 2}, ans {1};
 
	while (start <= end) {
		int mid {(start + end) / 2};
 
		if (cw(points[0], points[mid], t)) {
            ans = mid;
 
			start = mid + 1;
		} else {
			end = mid - 1;
		}
	}
 
	return ans;
}
 
// -1 - outside, 0 - inside, 1 - boundary
template <typename T>
int point_in_polygon(const vector<Point2D<T>> &points, const Point2D<T> &t, bool include_collinear = false) {
    if (include_collinear && points.size() < 3) {
        return point_in_segment(points[0], points[1], t) ? 1 : -1;
    } else if (include_collinear && point_in_segment(points[0], points[1], t)) {
        return 1;
    } else if (include_collinear && point_in_segment(points[0], points.back(), t)) {
        return 1;
    }
 
	int region {get_region(points, t)};
 
	if (region == 0) {
		return -1;
	}
 
    if (include_collinear && point_in_segment(points[region], points[region + 1], t)) {
        return 1;
    }
 
	return cw(points[region], points[region + 1], t) ? 0 : -1;
}
```

---

> [!info] Objetivo
> - Tem como objetivo descobrir se um ponto $t$ está dentro, fora ou em cima de uma aresta de um polígono. Ademais, utiliza o [[Point2D]] e suas funções [[Collinear]] e [[Counter clockwise]].

> [!note]- Complexidade
> - $O(n)$

```cpp
// -1 - outside, 0 - inside, 1 - boundary
template <typename T>
int point_in_polygon(const vector<Point2D<T>> &points, const Point2D<T> &t) {
    int n {(int) points.size()};
    int w {};
 
    for (int i {}; i < n; ++i) {
        if (points[i] == t) {
            return 1;
        }
 
        int ne {i + 1 == n ? 0 : i + 1};

        if (points[i].y == t.y && points[ne].y == t.y) {
            if (min(points[i].x, points[ne].x) <= t.x && t.x <= max(points[i].x, points[ne].x)) {
                return 1;
            }
        } else {
            bool below {points[i].y  < t.y};

            if (below != (points[ne].y < t.y)) {
                if (collinear(points[i], t, points[ne])) {
                    return 1;
                }

                if (below == ccw(points[i], t, points[ne])) {
                    w += below ? 1 : -1;
                }
            }
        }
    }

    return w == 0 ? -1 : 0;
}
```

---