> [!info] Objetivo
> - Tem como objetivo realizar o hashing de strings, pois quando queremos comparar duas strings $a$ e $b$ obtemos uma complexidade de $min(|a|, |b|)$, porém se transformarmos essas strings em números através de um hashing podemos comparar esses números em $O(1)$.

> [!attention] Atenção
> - É bom que $p$ seja um número primo maior ou igual ao número de letras do alfabeto da questão. Se o alfabeto contém apenas letras minúsculas, ou seja, letras de [a..z], $p = 31$ é uma boa escolha. Porém, se o alfabeto contém tanto letras minúsculas quanto maiúsculas, ou seja, letras de [a..z] e [A..Z], $p = 53$ é uma boa escolha.
> - É bom que $m$ seja um número grande primo já que a probabilidade de termos uma colisão é de aproximadamente $\dfrac{1}{m}$,  geralmente $m = 1e9 + 9$ ou $m = 1e9 + 7$ são boas escolhas. 
> - Para diminuir a probabilidade de colisão é possível fazer um pair com dois hashes feitos com módulos diferentes

> [!note]- Complexidade
> - Build: $O(n)$
> - Substring hash: $O(1)$

```cpp
typedef unsigned long long ull;
typedef unsigned int ui;

class StringHashing {
public:
	StringHashing(const string &s): hs(s.size()), p(s.size()) {
		this->p[0] = 1;
		this->hs[0] = this->get_int(s[0]);
		
		for (int i {1}; i < (int) s.size(); ++i) {
			this->p[i] = this->mod_mul(this->p[i - 1], this->base);
			this->hs[i] = (this->mod_mul(this->hs[i - 1], this->base) + this->get_int(s[i])) % this->MOD;
		}
	}

	// 0-indexed
	ull operator()(int l, int r){
		ull res {this->hs[r]};
		
		if (l > 0) {
			res = (res + this->MOD - this->mod_mul(this->p[r - l + 1], this->hs[l - 1])) % this->MOD;
		}
		
		return res;
	}

private:
	const ull MOD {(1LL << 61) - 1};
	const int base {31};
	vector<ull> hs, p;

	ull mod_mul(ull a, ull b) {
		ull l1 {(ui) a}, l2 {(ui) b};
		ull h1 {a >> 32}, h2 {b >> 32};
		ull l {l1 * l2}, m {l1 * h2 + l2 * h1}, h {h1 * h2};
		ull ret {(l & this->MOD) + (l >> 61) + (h << 3) + (m >> 29) + ((m << 35) >> 3) + 1};
		
		ret = (ret & this->MOD) + (ret >> 61);
		ret = (ret & this->MOD) + (ret >> 61);
		
		return ret - 1;
	}
	
	int get_int(char ch) {
		return ch - 'a' + 1;
	}
};
```

---