```ad-info
title: Objetivo

- É uma estrutura de dados que suporta consultas sobre intervalos e atualizações em apenas um índice ou atualizações em um intervalo e perguntas sobre um índice. Caso as duas operações sejam para fazer em intervalos a [[Segment tree with lazy propagation]] é uma melhor escolha.
```

```ad-note
title: Complexidade
collapse: true

- Build: $O(n)$ para implementação de consulta com intervalos e atualizações em índice ou $O(n \log n)$ para implementação com atualizações em intervalo e consultas em índice.
- Query/update: $O(\log n)$
```

`````ad-example
title: BIT com atualizações em índices e perguntas sobre um intervalo $[L, R]$.

- A implementação abaixo mostra uma BIT capaz de somar $x$ em um elemento $i$ qualquer do intervalo $[1, N]$ ou de dizer qual a soma dos elementos no intervalo $[L, R]$.

```cpp
#include <bits/stdc++.h>

using namespace std;

#define MAXN int(1e5)

int n;
int BIT[MAXN];

int query(int i) {
    int sum {};

    for (; i > 0; i -= i & -i) {
        sum += BIT[i];
    }

    return sum;
}

int range_query(int l, int r) {
    return query(r) - query(l - 1);
}

void update(int i, int x) {
    for (; i <= n; i += i & -i) {
        BIT[i] += x;
    }
}

int main() {
	int q;

	cin >> n >> q;

    for (int i {1}; i <= n; ++i) {
        int aux;

        cin >> aux;

        update(i, aux);
    }

	for (int i {}; i < q; ++i) {
		int op;

		cin >> op;

		if (op == 1) {
			int l, r;

			cin >> l >> r;

			cout << range_query(l, r) << '\n';
		} else {
			int p, x;

			cin >> p >> x;

			update(p, x);
		}
	}

	return 0;
}
```
`````

`````ad-example
title: BIT com atualizações em intervalos $[L, R]$ e perguntas sobre um índice qualquer.

- A implementação abaixo mostra uma BIT capaz de fazer o xor de $x$ em todos os elementos de um intervalo $[L, R]$ ou de dizer qual o valor de um elemento $i$ qualquer do intervalo $[1, N]$.

```cpp
#include <bits/stdc++.h>

using namespace std;

#define MAXN int(1e5) * 3 + 10

int n;
int BIT[MAXN];

void update(int idx, int val) {
    for (; idx <= n; idx += idx & -idx) {
        BIT[idx] ^= val;
    }
}

void range_update(int l, int r, int val) {
    update(l, val);
    update(r + 1, val);
}

int point_query(int idx) {
    int ans {};

    for (; idx > 0; idx -= idx & -idx) {
        ans ^= BIT[idx];
    }

    return ans;
}

int main() {
    int q;

    cin >> n >> q;

    for (int i {1}; i <= n; ++i) {
        int aux;

        cin >> aux;

        range_update(i, i, aux);
    }

    for (int i {}; i < q; ++i) {
        int op, l, r;

        cin >> op;

        if (op == 1) {
            int l, r, x;

            cin >> l >> r >>x;

            range_update(l, r, x);
        } else {
            int pq;

            cin >> pq;

            cout << point_query(pq) << '\n';
        }
    }

    return 0;
}
```
`````

---