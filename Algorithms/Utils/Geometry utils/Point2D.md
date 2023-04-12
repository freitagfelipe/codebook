```ad-info
title: Objetivo

- Apresentar uma implementação de um ponto 2D.
```

```cpp
template <typename T>
struct Point2D {
    T x;
    T y;
    
    Point2D(T x, T y) {
	    this->x = x;
	    this->y = y;
    }
    
    Point2D& operator+=(const Point2D &t) {
        this->x += t.x;
        this->y += t.y;

        return *this;
    }
    
    Point2D& operator-=(const Point2D &t) {
        this->x -= t.x;
        this->y -= t.y;
        
        return *this;
    }
    
    Point2D& operator*=(T t) {
        this->x *= t;
        this->y *= t;
        
        return *this;
    }
    
    Point2D& operator/=(T t) {
        this->x /= t;
        this->y /= t;
        
        return *this;
    }
    
    Point2D operator+(const Point2D &t) const {
        return Point2D(*this) += t;
    }
    
    Point2D operator-(const Point2D &t) const {
        return Point2D(*this) -= t;
    }
    
    Point2D operator*(T t) const {
        return Point2D(*this) *= t;
    }
    
    Point2D operator/(T t) const {
        return Point2D(*this) /= t;
    }
};

template <typename T>
T dot(const Point2D<T> &a, const Point2D<T> &b) {
	return a.x * b.x + a.y * b.y;
}

template <typename T>
T cross(const Point2D<T> &a, const Point2D<T> &b) {
	return a.x * b.y - a.y * b.x;
}

template <typename T>
T norm(const Point2D<T> &a) {
	return dot(a, a);
}

template <typename T>
double length(const Point2D<T> &a) {
	return sqrt(norm(a));
}

template <typename T>
double projection(const Point2D<T> &a, const Point2D<T> &b) {
	return dot(a, b) / length(b);
}

template <typename T>
double angle(const Point2D<T> &a, const Point2D<T> &b) {
	return acos(dot(a, b) / length(a) / length(b));
}

template <typename T>
bool clockwise(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c) {
	return cross((b - a), (c - a)) < 0;
}

template <typename T>
bool intersect(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &c, const Point2D<T> &d) {
	bool first_condition {clockwise(a, b, c) != clockwise(a, b, d)};
	bool second_condition {clockwise(c, d, a) != clockwise(c, d, b)};

	return (first_condition && second_condition);
}

template <typename T>
double distance_between_points(const Point2D<T> &a, const Point2D<T> &b) {
	T dx {a.x - b.x};
	T dy {a.y - b.y};

	return sqrt(dx * dx + dy * dy);
}

// Consegue calcular a distância de um ponto p até uma reta r descrita pelos pontos a e b.
template <typename T>
double distance_between_line_and_point(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &p) {
	Point2D<T> ab {b - a}, ap {p - a};

	T distance {abs(cross(ap, ab))};

	return distance / distance_between_points(a, b);
}

// Consegue calcular a distância de um ponto p até um segmento de reta r descrito pelos pontos a e b.
template <typename T>
double distance_between_segment_and_point(const Point2D<T> &a, const Point2D<T> &b, const Point2D<T> &p) {
	if (dot(p - a, b - a) < 0) {
		return distance_between_points(p, a);
	} else if (dot(p - b, a - b) < 0) {
		return distance_between_points(p, b);
	}

	return distance_between_line_and_point(a, b, p);
}
```

---