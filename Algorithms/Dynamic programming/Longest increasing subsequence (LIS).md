> [!info] Objetivo
> - Tem como objetivo encontrar qual é a maior subsequência crescente do vetor $v$.

> [!note]- Complexidade
> - $O(n \log n)$

> [!hint] Encontrando a maior subsequência não decrescente
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

---