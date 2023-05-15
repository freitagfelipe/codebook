```cpp
template <typename T>
double angle(const Point3D<T> &a, const Point3D<T> &b) {
	return acos(dot(a, b) / length(a) / length(b));
}
```

---