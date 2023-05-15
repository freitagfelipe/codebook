```cpp
template <typename T>
bool intersect(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, const Point2D<T> &d) {
	bool first_condition {cw(a, b, c) != cw(a, b, d)};
	bool second_condition {cw(c, d, a) != cw(c, d, b)};

	return first_condition && second_condition;
}

```

---