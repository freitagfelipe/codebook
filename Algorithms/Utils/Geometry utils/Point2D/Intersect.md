> [!info] Objetivo
> - Verificar se dois segmentos descritos pelos pontos $\vec{ab}$ e $\vec{cd}$ estão ou não se cruzando utilizando [[Point2D]] e sua função [[Clockwise]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
bool intersect(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, const Point2D<T> &d) {
	bool first_condition {cw(a, b, c) != cw(a, b, d)};
	bool second_condition {cw(c, d, a) != cw(c, d, b)};

	return first_condition && second_condition;
}
```

---