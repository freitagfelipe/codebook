> [!info] Objetivo
> Resolver o problema da soma máxima de um intervalo, ou seja, dado um vetor $v$ ele encontra uma subsequência de $v$ que tenha a maior soma.

> [!faq] Como funciona?
> Iníciamos uma $soma$ e uma $resposta$ com o valor do primeiro elemento do vetor, pois na primeira iteração ele é a resposta, e iremos iterar pelos elementos do vetor começando do primeiro elemento e a cada iteração faremos uma pergunta se vale a pena adicionar o i-ésimo elemento na soma ou não, ou seja, se vale mais a pena iniciar uma nova soma, caso a resposta seja afirmativa basta atribuir o i-ésimo elemento a variável soma, caso ela seja negativa basta somarmos o i-ésimo elemento a variável soma e após cada um desses passos a resposta será o máximo entre a soma atual ou a própria resposta.

> [!note]- Complexidade
> $O(n)$, pois o laço é linear e só realiza operações constantes.

```cpp
int kadane(const vector<int> &v) {
    int sum {v[0]};
    int ans {v[0]};

    for (int i {1}; i < v.size(); ++i) {
        sum = max(v[i], sum + v[i]);
        ans = max(ans, sum);
    }

    return ans;
}
```

> [!hint] Adaptação
> O algoritmo de Kadane pode ser adaptado para encontrar o início e o fim da sequência como mostrado logo abaixo.

> [!faq] Como funciona?
> Teremos um vetor DP que lembrará a melhor resposta na i-ésima iteração e um vetor $opt$ para salvar em qual elemento começa a sequência ótima que o i-ésimo elemento está inserido, como na primeira iteração a melhor resposta é o elemento na posição zero iniciaremos o a $DP$ na primeira posição com o elemento do vetor na posição zero e o $opt$ na primeira posição com o valor zero, pois é nesse elemento que começa a sequência ótima. Agora basta que iteremos pelo vetor começando do primeiro elemento e repetiremos o mesmo processo do algoritmo base, perguntaremos se vale a pena adicionar o i-ésimo elemento na soma ou não, ou seja, se é melhor iniciar uma nova soma, caso a resposta seja afirmativa adicionaremos o i-ésimo elemento na soma e diremos que o $opt[i] = opt[i - 1]$, pois o $opt[i - 1]$ irá nos dizer onde começa a soma que ele agora faz parte, caso a resposta seja negativa iniciaremos uma nova soma e faremos $opt[i] = i$ para dizer que a soma atual começa nesse elemento. Ao final disso, procuraremos pela resposta na $DP$ e guardaremos o índice da resposta na variável $optimal$, pois o índice de início da sequência será $opt[optimal]$ e o fim será na posição $optimal$.

> [!note]- Complexidade
> $O(n)$, pois ambos os laços são lineares e realizam apenas operações constantes.

```cpp
typedef pair<int, int> pii;

pii kadane(const vector<int> &v) {
	vector<int> DP(v.size());
	vector<int> opt(v.size());
	
    DP[0] = v[0];
    opt[0] = 0;
    
    for (int i {1}; i < v.size(); ++i) {
        if (v[i] >= v[i] + DP[i - 1]) {
            opt[i] = i;
        } else {
            opt[i] = opt[i - 1];
        }
    
        DP[i] = max(v[i], DP[i - 1] + v[i]);
    }

    int answer {DP[0]}, optimal {};
    
    for (int i {1}; i < v.size(); ++i) {
        if (answer < DP[i]) {
            answer = DP[i];
            optimal = i;
        }
    }

    return {opt[optimal], optimal};
}
```

---