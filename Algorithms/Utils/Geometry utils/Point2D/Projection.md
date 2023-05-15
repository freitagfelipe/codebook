```cpp
template <typename T>
double projection(const Point2D<T> &a, const Point2D<T> &b) {
	return dot(a, b) / length(b);
}
```

---