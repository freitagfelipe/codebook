```cpp
template <typename T>
bool cw(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, bool include_collinear = false) {
    int result {orientation(a, b, c)};

    return result < 0 || (include_collinear && result == 0);
}
```

---