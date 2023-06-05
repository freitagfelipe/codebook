> [!info] Objetivo
> - Calcular o produto escalar entre os vetores $\vec{a}$ e $\vec{b}$ utilizando [[Point2D]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
T dot(const Point2D<T> &a, const Point2D<T> &b) {
	return a.x * b.x + a.y * b.y;
}
```

---