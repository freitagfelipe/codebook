> [!info] Objetivo
> - A stack query tem como objetivo responder de maneira eficiente qual o menor elemento e qual o maior elemento em uma stack.

> [!note]- Complexidade
> - Push/pop: $O(1)$
> - Min/max: $O(1)$
> - Top: $O(1)$
> - Empty: $O(1)$

> [!hint] Adaptação para uma queue
> - É possível utilizar essa estrutura para realizar queries em queue, basta criar duas stack query e na primeira você só remove e da segunda você só adiciona e quando a primeira estiver vazia você passa todos os elementos da segunda para a primeira.

```cpp
template <typename T>
struct StackQuery {
public:
    void push(T x) {
        if (this->smin.empty()) {
            this->smin.push_back(x);
        } else {
            this->smin.push_back(::min(this->smin.back(), x));
        }

        if (this->smax.empty()) {
            this->smax.push_back(x);
        } else {
            this->smax.push_back(::max(this->smax.back(), x));
        }

        this->s.push_back(x);
    }

    void pop() {
	    if (this->empty()) {
			throw runtime_error("Stack query size == 0");
	    }
	
        this->smin.pop_back();
        this->smax.pop_back();
        this->s.pop_back();
    }

    bool empty() {
        return s.empty();
    }

    T top() {
	    if (this->empty()) {
			throw runtime_error("Stack query size == 0");
	    }

        return s.back();
    }

    T min() {
	    if (this->empty()) {
			throw runtime_error("Stack query size == 0");
	    }
	    
        return this->smin.back();
    }

    T max() {
	    if (this->empty()) {
			throw runtime_error("Stack query size == 0");
	    }
	    
        return this->smax.back();
    }

private:
    vector<T> smax;
    vector<T> smin;
    vector<T> s;
};
```

---