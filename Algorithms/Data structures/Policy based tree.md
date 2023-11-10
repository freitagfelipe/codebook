> [!info] Objetivo
> - Essas estruturas conseguem fazer as mesmas coisas das estruturas $multimap$ e $set$, mas com duas operações adicionais que podem ser úteis dependendo do problema.

> [!note]- Complexidade
> - Find by order: $O(\log n)$
> - Order of key: $O(\log n)$

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>

using namespace std;
using namespace __gnu_pbds;

// Accepts the following operations:
//      find_by_order(x): k-th element in a set (0-indexed)
//      order_of_key(x): number of items strictly smaller than k
template <typename T>
using ordered_set = tree<T, null_type, less<T>, rb_tree_tag, tree_order_statistics_node_update>;
template <typename K, typename V>
using ordered_multimap = tree<K, V, less<K>, rb_tree_tag, tree_order_statistics_node_update>;
```

---