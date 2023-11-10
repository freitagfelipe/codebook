> [!info] Objetivo
> - Tem como objetivo dizer se um dois vetores $\vec{b}$ e $\vec{c}$ centrados no ponto $a$ são colineares utilizando [[Point2D]] e sua função [[Orientation]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
bool collinear(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
    return orientation(a, b, c) == 0;
}
```

---