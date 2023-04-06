```ad-info
title: Objetivo

- Apresentar uma implementação de um ponto 3D.
```

```cpp
template <typename T>
struct Point3D {
    T x;
    T y;
    T z;
    
    Point3D(T x, T y, T z) {
	    this->x = x;
	    this->y = y;
	    this->z = z;
    }
    
    Point3D& operator+=(const Point3D &t) {
        x += t.x;
        y += t.y;
        z += t.z;
        
        return *this;
    }
    
    Point3D& operator-=(const Point3D &t) {
        x -= t.x;
        y -= t.y;
        z -= t.z;
        
        return *this;
    }
    
    Point3D& operator*=(T t) {
        x *= t;
        y *= t;
        z *= t;
        
        return *this;
    }
    
    Point3D& operator/=(T t) {
        x /= t;
        y /= t;
        z /= t;
        
        return *this;
    }
    
    Point3D operator+(const Point3D &t) const {
        return Point3D(*this) += t;
    }
    
    Point3D operator-(const Point3D &t) const {
        return Point3D(*this) -= t;
    }
    
    Point3D operator*(T t) const {
        return Point3D(*this) *= t;
    }
    
    Point3D operator/(T t) const {
        return Point3D(*this) /= t;
    }
};

template <typename T>
T dot(const Point3D<T> &a, const Point3D<T> &b) {
    return a.x * b.x + a.y * b.y + a.z * b.z;
}

template <typename T>
Point3D<T> cross(Point3D<T> &a, Point3D<T> &b) {
    return Point3D(a.y * b.z - a.z * b.y,
                   a.z * b.x - a.x * b.z,
                   a.x * b.y - a.y * b.x);
}

template <typename T>
T norm(const Point3D<T> &a) {
	return dot(a, a);
}

template <typename T>
double length(const Point3D<T> &a) {
	return sqrt(norm(a));
}

template <typename T>
double projection(const Point3D<T> &a, const Point3D<T> &b) {
	return dot(a, b) / length(b);
}

template <typename T>
double angle(const Point3D<T> &a, const Point3D<T> &b) {
	return acos(dot(a, b) / length(a) / length(b));
}
```

---