> [!info] Objetivo
> - Tem como objetivo determinar o número de pares $(i, j)$, com $i < j$, de uma sequência, tal que $a_i > a_j$. O algoritmo irá usar uma adaptação do [[Merge sort]]. Também é possível resolver esse problema utilizando [[Fenwick tree (BIT)]] junto da técnica de  [[Coordinate compression]] se necessário.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
typedef long long ll;

ll count(vector<int> &v, int start, int end) {
	ll ans {};
    vector<int> result;

    int p1 {start}, mid {(start + end) / 2}, p2 {mid + 1};

    while (p1 <= mid && p2 <= end) {
        if (v[p1] <= v[p2]) {
            result.push_back(v[p1++]);
        } else {
			ans += mid - p1 + 1;

            result.push_back(v[p2++]);
        }
    }

    while (p1 <= mid) {
        result.push_back(v[p1++]);
    }

    while (p2 <= end) {
        result.push_back(v[p2++]);
    }

    copy(result.begin(), result.end(), v.begin() + start);

	return ans;
}

ll inversions_count(vector<int> &v, int start, int end) {
    ll ans {};
    
    if (end > start) {
        int mid {(start + end) / 2};

        ans += inversions_count(v, start, mid);
        ans += inversions_count(v, mid + 1, end);

        ans += count(v, start, end);
    }
    
    return ans;
}
```

---