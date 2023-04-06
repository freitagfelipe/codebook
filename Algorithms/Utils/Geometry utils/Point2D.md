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
```

---