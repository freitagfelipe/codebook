```cpp
template <typename T>
Point2D<double> rotate_point(const Point2D<T> &p, double theta) {
	auto [x, y] = p;

	double new_x {x * cos(theta) - y * sin(theta)};
	double new_y {x * sin(theta) + y * cos(theta)};

	return Point2D<double>(new_x, new_y);
}
```

---