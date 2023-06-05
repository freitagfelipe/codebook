> [!info] Objetivo
> - Se parece muito com a técnica de [[Line sweep]], porém ao invés de termos uma linha se movendo pelo eixo $x$ ou pelo eixo $y$, temos uma semirreta centrada na origem do plano sendo rotacionada no sentido horário ou anti-horário, a semirreta pode ser trocada também por uma reta. A implementação deste algoritmo utiliza o [[Point2D]] e suas funções [[Algorithms/Utils/Geometry utils/Point2D/Cross product|Cross product]] e [[Algorithms/Utils/Geometry utils/Point2D/Norm|Norm]]. O código apresentado mostra apenas como ordenar os eventos.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
template <typename T>
int region_value(const Point2D<T> &a) {
	if (a.y > 0 || (a.y == 0 && a.x > 0)) {
		return 0;
	}

	return 1;
}

template <typename T>
bool cmp(const Point2D<T> &a, const Point2D<T> &b) {
	int a_region_value {region_value(a)};
	int b_region_value {region_value(b)}

	if (a_region_value != b_region_value) {
		return a_region_value < b_region_value;
	}

	T cross_result {cross(a, b)};

	if (cross_result != 0) {
		return cross_result > 0;
	}

	return norm(a) < norm(b);
}
```

`````ad-example
title: Exemplo com a questão [Jogo](https://neps.academy/br/exercise/381) da seletiva para IOI 2017.

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;

// MAXN is the largest possible number of points
#define MAXN 3010

template <typename T>
struct Point2D {
    T x;
    T y;
    T pontuation;

    Point2D() = default;

    Point2D &operator-=(const Point2D &t) {
        this->x -= t.x;
        this->y -= t.y;
        
        return *this;
    }

    Point2D operator-(const Point2D &t) const {
        return Point2D(*this) -= t;
    }
};

template <typename T>
T dot(const Point2D<T> &a, const Point2D<T> &b) {
	return a.x * b.x + a.y * b.y;
}

template <typename T>
T norm(const Point2D<T> &a) {
	return dot(a, a);
}

template <typename T>
T cross(const Point2D<T> &a, const Point2D<T> &b) {
	return a.x * b.y - a.y * b.x;
}

template <typename T>
int region_value(const Point2D<T> &a) {
	if (a.y > 0 || (a.y == 0 && a.x > 0)) {
		return 0;
	}

	return 1;
}

template <typename T>
bool cmp(const Point2D<T> &a, const Point2D<T> &b) {
	if (region_value(a) != region_value(b)) {
		return region_value(a) < region_value(b);
	}

    T cross_result {cross(a, b)};

	if (cross_result != 0) {
		return cross_result > 0;
	}

	return norm(a) < norm(b);
}

Point2D<ll> points[MAXN], centralized_points[MAXN];

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int n;

    cin >> n;

    for (int i {}; i < n; ++i) {
        cin >> points[i].x >> points[i].y >> points[i].pontuation;
    }

    ll ans {LONG_LONG_MIN};

    for (int i {}; i < n; ++i) {
        int centralized_size {};

        for (int j {}; j < n; ++j) {
            if (j == i) {
                continue;
            }
            
            centralized_points[centralized_size++] = points[j] - points[i];

            if (region_value(centralized_points[centralized_size - 1])) {
                --centralized_size;
            }
        }

        sort(centralized_points, centralized_points + centralized_size, cmp<ll>);

        for (int j {}; j < centralized_size; ++j) {
            ll current_sum {points[i].pontuation};
            int p1 {j};

            while (p1 < centralized_size && cross(centralized_points[j], centralized_points[p1]) == 0) {
                current_sum += centralized_points[p1].pontuation;

                ans = max(ans, current_sum);

                ++p1;
            }

            j = p1 - 1;
        }
    }

    cout << ans << '\n';

    return 0;
}
```
`````

---