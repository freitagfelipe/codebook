```cpp
template <typename T>
double projection(const Point3D<T> &a, const Point3D<T> &b) {
	return dot(a, b) / length(b);
}
```

---