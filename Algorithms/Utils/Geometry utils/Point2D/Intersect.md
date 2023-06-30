> [!info] Objetivo
> - Verificar se dois segmentos descritos pelos pontos $\vec{ab}$ e $\vec{cd}$ estão ou não se cruzando utilizando [[Point2D]] e sua função [[Orientation]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
bool intersect_aux(T a, T b, T c, T d) {
    if (a > b) {
        swap(a, b);
    }

    if (c > d) {
        swap(c, d);
    }

    return max(a, c) <= min(b, d);
}

template <typename T>
bool intersect(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, const Point2D<T> &d) {
    if (orientation(c, a, d) == 0 && orientation(c, b, d) == 0) {
        return intersect_aux(a.x, b.x, c.x, d.x) && intersect_aux(a.y, b.y, c.y, d.y);
    }

    bool first_condition(orientation(a, b, c) != orientation(a, b, d));
    bool second_condition(orientation(c, d, a) != orientation(c, d, b));

    return first_condition && second_condition;
}
```

---