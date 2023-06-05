> [!info] Objetivo
> - Calcular o produto vetorial entre os vetores $\vec{a}$ e $\vec{b}$ utilizando [[Point2D]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
T cross(const Point2D<T> &a, const Point2D<T> &b) {
	return a.x * b.y - a.y * b.x;
}
```

---