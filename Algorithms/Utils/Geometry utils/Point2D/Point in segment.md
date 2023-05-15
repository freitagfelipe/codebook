```cpp
template <typename T>
bool point_in_segment(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
	if (cross(b - a, c - a) != 0) {
		return false;
	}

	if (min(a.x, b.x) > c.x || c.x > max(a.x, b.x)) {
		return false;
	} else if (min(a.y, b.y) > c.y || c.y > max(a.y, b.y)) {
		return false;
	}

	return true;
}
```

---