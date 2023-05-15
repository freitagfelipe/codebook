```cpp
template <typename T>
double angle(const Point2D<T> &a, const Point2D<T> &b) {
	return acos(dot(a, b) / length(a) / length(b));
}
```

---