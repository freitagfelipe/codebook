> [!info] Objetivo
> - Encontrar a maior subsequência crescente de um vetor.

> [!note]- Complexidade
> - $O(n \log n)$

> [!hint] Encontrar a maios subsequência não decrescente
> - Caso a questão peça para encontrar a maior subsequência não decrescente é só ao invés de procurar um $lower\_bound(v[i])$ procurar por um $upper\_bound(v[i])$.

```cpp
size_t lis(const vector<int> &v) {
	vector<int> stacks;

	for (int num : v) {
		vector<int>::iterator it {lower_bound(stacks.begin(), stacks.end(), num)};

		if (it == stacks.end()) {
			stacks.push_back(num);
		} else {
			*it = num;
		}
	}

	return stacks.size();
}
```

> [!hint] Retornar a maior subsequência crescente
> - O código abaixo pode ser utilizado para retornar a LIS encontrada no vetor.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
vector<int> lis(const vector<int> &v) {
	vector<int> stacks;
	vector<int> p;
	vector<int> pos(v.size());

	for (int i {}; i < v.size(); ++i) {
		vector<int>::iterator it {lower_bound(stacks.begin(), stacks.end(), v[i])};

        long int dist {it - stacks.begin()};

		if (it == stacks.end()) {
			stacks.push_back(v[i]);
		} else {
			*it = v[i];
		}

        pos[dist] = i;

        p.push_back(dist == 0 ? -1 : pos[dist - 1]);
	}

    if (stacks.size() == 0) {
        return {};
    }

    vector<int> lis;

    int i {pos[int(stacks.size()) - 1]};

    while (i >= 0) {
        lis.push_back(v[i]);

        i = p[i];
    }

    reverse(lis.begin(), lis.end());

    return lis;
}
```

---