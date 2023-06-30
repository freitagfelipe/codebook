> [!info] Objetivo
> - Tem como objetivo calcular todos as substrings palindrômicas em uma string.

> [!note]- Complexidade
> - $O(n)$

```cpp
vector<int> manacher(const string &s) {
    int n {(int) s.size()};

    vector<int> d1(n);

    int l {}, r {-1};

    for (int i {}; i < n; ++i) {
        int k {i > r ? 1 : min(d1[l + r - i], r - i + 1)};

        while (i + k < n && i - k >= 0 && s[i + k] == s[i - k]) {
            ++k;
        }

        d1[i] = k;

        if (i + k - 1 > r) {
            l = i - k + 1;
            r = i + k - 1;
        }
    }

    vector<int> d2(n);

    l = 0;
    r = -1;

    for (int i {}; i < n; ++i) {
        int k {i > r ? 0 : min(d2[l + r - i + 1], r - i + 1)};

        while (i + k < n && i - k - 1 >= 0 && s[i + k] == s[i - k - 1]) {
            ++k;
        }

        d2[i] = k;

        if (i + k - 1 > r) {
            l = i - k;
            r = i + k - 1;
        }
    }

    vector<int> ans(n * 2 - 1);

    for (int i {}; i < n; ++i) {
        ans[2 * i] = 2 * d1[i] - 1;
    }

    for (int i {}; i < n - 1; ++i) {
        ans[2 * i + 1] = 2 * d2[i + 1];
    }

    return ans;
}
```

> [!hint] Verificar se uma substring é um palíndromo
> - Dado o vetor feito pela função manacher e os índices da substring tal que $i, j \in [0..n - 1]$ a função retorna true se a string for um palíndromo e false caso contrário.

> [!note]- Complexidade
> - $O(1)$

```cpp
bool is_palindrome(const vector<int> &m, int i, int j) {
	return m[i + j] >= j - i + 1;
}
```

> [!hint] Procurar a maior string que é um palíndromo
> - Dado o vetor feito pela função manacher a função irá retornar um par $f, s \in [0..n - 1]$ tal que a substring $s[i..j]$ é o maior palíndromo da string $s$.

> [!note]- Complexidade
> - $O(n)$

```cpp
typedef pair<int, int> pii;

pii longest_palindrome(const vector<int> &m) {
	int ans {}, length {};

	for (int i {}; i < (int) m.size(); ++i) {
		if (m[i] > length) {
			length = m[i];
			ans = i;
		}
	}

	length /= 2;

	if (ans % 2 == 0) {
		ans /= 2;

		return {ans - length, ans + length};
	}

	ans += 1;
	ans /= 2;

	return {ans - length, ans + length - 1};
}
```

---