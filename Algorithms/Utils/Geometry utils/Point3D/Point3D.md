> [!info] Objetivo
> - Apresentar uma implementação básica e genérica de um Point3D e algumas funções que a utilizam.

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
```

> [!summary] Lista de funções que a utilizam
> - [[Algorithms/Utils/Geometry utils/Point3D/Angle|Angle]]
> - [[Algorithms/Utils/Geometry utils/Point3D/Cross product|Cross product]]
> - [[Algorithms/Utils/Geometry utils/Point3D/Dot product|Dot product]]
> - [[Algorithms/Utils/Geometry utils/Point3D/Length|Length]]
> - [[Algorithms/Utils/Geometry utils/Point3D/Norm|Norm]]
> - [[Algorithms/Utils/Geometry utils/Point3D/Projection|Projection]]

---