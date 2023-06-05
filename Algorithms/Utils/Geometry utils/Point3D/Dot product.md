> [!info] Objetivo
> - Calcular o produto escalar entre os vetores $\vec{a}$ e $\vec{b}$ utilizando [[Point3D]].

> [!note]- Complexidade
> - $O(1)$

```cpp
template <typename T>
T dot(const Point3D<T> &a, const Point3D<T> &b) {
    return a.x * b.x + a.y * b.y + a.z * b.z;
}
```

---