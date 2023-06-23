> [!info] Objetivo
> - Calcular de maneira eficiente o array de prefixo e alguns outros usos que serão mostrados ao longo da página.

> [!note]- Complexidade
> - $O(n)$

```cpp
vector<int> kmp(const string &s) {
	vector<int> pi(s.size());

	for (int i {1}, j {}; i < (int) s.size(); ++i) {
		while (j > 0 && s[i] != s[j]) {
			j = pi[j - 1];
		}

        if (s[i] == s[j]) {
            ++j;
        }

		pi[i] = j;
	}

    return pi;
}
```

> [!hint] Calcular matches de um padrão em um texto
> - Verificar em quais posições ocorrem o match do padrão $s$ no texto $t$. Além dessa implementação também seria possível adaptar a função de prefixo passando a string $s + \# + t$ e em todo momento que $pi[i] = |s|$ nós encontramos um match.

```cpp
vector<int> ocurrences(const string &s, const string &t) {
	vector<int> pi {kmp(s + "#")}, matches;

	for (int i {}, j {}; i < (int) t.size(); ++i) {
		while (j > 0 && t[i] != s[j]) {
			j = pi[j - 1];
		}

		if (t[i] == s[j]) {
			++j;
		}

		if (j == (int) s.size()) {
			matches.push_back(i - j + 1);
		}
	}

	return matches;
}
```

> [!hint] Contando aparições de prefixos
> - Dado uma string $s$ de tamanho $n$ o problema é contar quantas vezes o prefixo $s[0..i]$ aparece na string $s$.

```cpp
vector<int> count_prefixes(const string &s) {
	int n {(int) s.size()};
	vector<int> ans(n + 1), pi {kmp(s)};

	for (int i {}; i < n; ++i) {
		++ans[pi[i]];
	}

	for (int i {n - 1}; i > 0; --i) {
		ans[pi[i - 1]] += ans[i];
	}

	for (int i {1}; i <= n; ++i) {
		ans[i - 1] = ans[i] + 1;
	}

	ans.pop_back();

	return ans;
}
```

> [!hint] Comprimindo strings
> - Dado uma string $s$ queremos encontrar uma string $t$ de tamanho mínimo tal que $s$ possa ser representada por uma concatenação de uma ou mais cópias de $t$.

```cpp
string compress(const string &s) {
	int n {(int) s.size()};
	vector<int> pi {kmp(s)};

	int k {n - pi.back()};

	if (n % k != 0) {
		return s;
	}

	return s.substr(0, k);
}
```

> [!hint] Autômato de KMP
> - Utilizando o autômato conseguimos descobrir os próximos valores de $j$ em tempo constante e resolver alguns problemas que não seriam possíveis sem ele.

```cpp
#define K 26

int get_id(char ch) {
	return ch - 'a';
}

vector<vector<int>> automaton(const string &s) {
	int n {(int) s.size()};

	vector<int> pi {kmp(s)};
	vector<vector<int>> aut(n + 1, vector<int>(K));

	aut[0][get_id(s[0])] = 1;

	for (int i {1}; i < n; ++i) {
		for (int c {}; c < K; ++c) {
			aut[i][c] = c == get_id(s[i]) ? i + 1 : aut[pi[i - 1]][c];
		}
	}

	for (int c {}; c < K; ++c) {
		aut[n][c] = aut[pi[n - 1]][c];
	}

	return aut;
}
```

---