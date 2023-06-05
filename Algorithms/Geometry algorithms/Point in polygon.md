> [!info] Objetivo
> - O algoritmo apresentado abaixo tem como objetivo descobrir se um ponto $t$ qualquer está estritamente dentro de um polígono estritamente convexo. Ademais, ele utiliza [[Point2D]] e suas funções [[Clockwise]], [[Point in segment]].

> [!caution] Restrição
> - Os pontos precisam estar ordenados em sentido horário.

> [!note]- Complexidade
> - $O(\log n)$

```cpp
template <typename T>
int get_region(const vector<Point2D<T>> &points, const Point2D<T> &t, bool include_collinear = false) {
    if (!cw(points[0], points[1], t, include_collinear)) {
        return 0;
    }

    if (!cw(points.back(), points[0], t, include_collinear)) {
        return 0;
    }

	int start {1}, end {(int) points.size() - 2}, ans {1};

	while (start <= end) {
		int mid {(start + end) / 2};

		if (cw(points[0], points[mid], t, include_collinear)) {
            ans = mid;

			start = mid + 1;
		} else {
			end = mid - 1;
		}
	}

	return ans;
}

template <typename T>
bool inside_polygon(const vector<Point2D<T>> &points, const Point2D<T> &t, bool include_collinear = false) {
    if (points.size() < 3) {
        return point_in_segment(points[0], points[1], t);
    }

	int region {get_region(points, t, include_collinear)};

	if (region == 0) {
		return false;
	}

    if (include_collinear && point_in_segment(points[0], points[region], t)) {
        return true;
    } else if (include_collinear && point_in_segment(points[0], points[region + 1], t)) {
        return true;
    } else if (include_collinear && point_in_segment(points[region], points[region + 1], t)) {
        return true;
    }

	return cw(points[region], points[region + 1], t);
}
```

---