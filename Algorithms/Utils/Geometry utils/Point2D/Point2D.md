> [!info] Objetivo
> - Apresentar uma implementação básica e genérica de um Point2D e algumas funções que a utilizam.

```cpp
template <typename T>
struct Point2D {
    T x;
    T y;

	Point2D() = default;
    
    Point2D(T x, T y) {
	    this->x = x;
	    this->y = y;
    }
    
    Point2D& operator+=(const Point2D &t) {
        this->x += t.x;
        this->y += t.y;

        return *this;
    }
    
    Point2D &operator-=(const Point2D &t) {
        this->x -= t.x;
        this->y -= t.y;
        
        return *this;
    }
    
    Point2D &operator*=(T t) {
        this->x *= t;
        this->y *= t;
        
        return *this;
    }
    
    Point2D &operator/=(T t) {
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
```

> [!summary]  Funções que a utilizam
> - [[Angle]]
> - [[Clockwise]]
> - [[Counter clockwise]]
> - [[Cross product]]
> - [[Distance between line and point]]
> - [[Distance between points]]
> - [[Distance between segment and point]]
> - [[Dot product]]
> - [[Intersect]]
> - [[Length]]
> - [[Norm]]
> - [[Orientation]]
> - [[Point in segment]]
> - [[Projection]]
> - [[Rotate point]]

---