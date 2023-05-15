```cpp
template <typename T>
Point3D<T> cross(Point3D<T> &a, Point3D<T> &b) {
    return Point3D(a.y * b.z - a.z * b.y,
                   a.z * b.x - a.x * b.z,
                   a.x * b.y - a.y * b.x);
}
```

---