> [!info] Objetivo
> - Dado um vetor de inteiros $v$  que contém números que podem estar em um intervalo muito grande, mas só temos, por exemplo, $10^5$ elementos, podemos converter todos os números de $v$ para números que estão no intervalo $[0, 10^5]$ mantendo a magnitude dos números originais em relação aos outros utilizando a compressão de coordenadas.

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