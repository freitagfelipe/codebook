> [!info] Objetivo
> - Imagine que temos um vetor de números que só podem ter no máximo até $10^5$ elementos e que o intervalo desses elementos é de $[10^{-9}, 10^9]$, podemos reduzir esse intervalo para $10^5$ elementos por meio da compressão de coordenadas, já que é suficiente para representá-los e representar sua magnitude um intervalo de $[0, 10^5]$.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
void coordinate_compression(vector<int> &v) {
	vector<int> aux(v);

	sort(aux.begin(), aux.end());

	unordered_map<int, int> ump;
	int cnt {1};

	for (int x : aux) {
		ump[x] = cnt++;
	}

	for (int &x : v) {
		x = ump[x];
	}
}
```

---