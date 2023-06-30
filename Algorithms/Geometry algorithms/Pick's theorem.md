> [!info] Objetivo
> - O teorema de Pick nos diz que $S = i + \frac{p}{2} - 1$, tal que $S$ é a área do polígono simples, no qual podemos descobrir usando [[Area of ​​a simple polygon - Shoelace]], $i$ é a quantidade de lattice points que estão estritamente contidos dentro do polígono e $p$ é a quantidade de lattice points que estão contidos nas arestas, para descobrir esse número precisaremos as vezes utilizar o [[Euclidean algorithm]]. O algoritmo demonstrado abaixo tem como objetivo descobrir $i$. Ademais, a implementação utiliza o [[Point2D]].

> [!note]- Complexidade
> - $O(n)$

```cpp
template <typename T>
ll calculate_lattice_points_in_edges(const vector<Point2D<T>> &polygon) {
    ll ans {};

    for (int i {}; i < (int) polygon.size(); ++i) {
		Point2D<T> q {i ? polygon[i - 1] : polygon.back()};
		Point2D<T> p {polygon[i]};

        if (p.x == q.x) {
            ans += abs(p.y - q.y) - 1;
        } else if (p.y == q.y) {
            ans += abs(p.x - q.x) - 1;
        } else {
            ans += gcd(abs(p.x - q.x), abs(p.y - q.y)) - 1;
        }
    }

    return ans + polygon.size();
}

template <typename T>
ll calculate_lattice_points_inside_polygon(const vector<Point2D<T>> &polygon) {
	T area {calculate_two_times_area(polygon)};
    ll lattice_points_in_edge {calculate_lattice_points_in_edges(polygon)};

    return (area - lattice_points_in_edge + 2) / 2; 
}
```

---