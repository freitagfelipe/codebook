> [!info] Objetivo
> - Encontrar o fecho convexo, ou seja, o menor polígono convexo tal que ele contenha todos os pontos, assim como o [[Monotone chain]]. A implementação utiliza [[Point2D]] e suas funções [[Orientation]], [[Algorithms/Utils/Geometry utils/Point2D/Norm|Norm]], [[Collinear]] e [[Clockwise]].

> [!attention] Atenção
> - A ponto base do algoritmo deve ser aquele com o menor $y$ e em caso de empate desempataremos pelo menor x.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
template <typename T>
vector<Point2D<T>> grahams_scan(vector<Point2D<T>> &points, bool include_collinear = false) {
    Point2D<T> base {*min_element(points.begin(), points.end())};

    sort(points.begin(), points.end(), [&base](const Point2D<T> &a, const Point2D<T> &b) {
        int o {orientation(base, a, b)};

        if (o == 0) {
            return norm(a - base) < norm(b - base);
        }

        return o < 0;
    });

    if (include_collinear) {
        int i {(int) points.size() - 1};

        while (i >= 0 && collinear(base, points[i], points.back())) {
            --i;
        }

        reverse(points.begin() + i + 1, points.end());
    }

    vector<Point2D<T>> hull;

    for (Point2D<T> pt : points) {
        while (hull.size() >= 2 && !cw(hull[hull.size() - 2], hull.back(), pt, include_collinear)) {
            hull.pop_back();
        }

        hull.push_back(pt);
    }

    return move(hull);
}
```

---