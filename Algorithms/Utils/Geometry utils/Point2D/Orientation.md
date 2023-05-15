```cpp
template <typename T>
int orientation(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
    T result {a.x * (b.y - c.y) + b.x * (c.y - a.y) + c.x * (a.y - b.y)};

    if (result < 0) {
        return -1; // cw
    } else if (result > 0) {
        return 1; // ccw
    }

    return 0;
}
```

---