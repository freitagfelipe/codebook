## Trick

```cpp
vector<string> s;

// Maneira errada
sort(all(s));

// Maneira correta
sort(all(s), [](string &a, string &b) {
	return a + b < b + a;
});
```

---