> [!info] Objetivo
> - Dado um conjunto de moedas ilimitadas dizer se um troco qualquer pode ser feito ou não.

> [!note]- Complexidade
> - $O(kn)$

```cpp
// MAXK is the maximum value that the change can have
int DP[MAXK];

bool can_make(int k, const vector<int> &coins) {
    if (k == 0) {
        return true;
    }

    if (k < 0) {
        return false;
    }

    if (DP[k] >= 0) {
        return DP[k];
    }

    for (int coin : coins) {
        if (can_make(k - coin, coins)) {
            return (DP[k - coin] = 1);
        }
    }

    return (DP[k] = 0);
}
```

---