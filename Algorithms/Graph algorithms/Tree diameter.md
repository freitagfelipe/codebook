> [!info] Objetivo
> Encontrar em um grafo acíclico e conexo, ou seja, uma árvore a distância máxima entre dois vértices desse grafo. A implementação do algoritmo utiliza uma adaptação da [[Depth-first search (DFS)]].

> [!faq] Como funciona?
> - Explicarei primeiro a DFS, ela será iniciada com uma distância $d$ igual a zero, pois a distância do primeiro nó até ele mesmo é zero e utilizaremos uma variável $p$ para lembrarmos quem chamou a recursão, pois se voltarmos em algum momento para o nó $p$ isso irá causar loop infinito e ela começará com um valor negativo, pois esse nó não existe. Feito isso, iremos para cada vizinho do nó atual chamar a recursão incrementado a distância em uma unidade e dizendo de qual nó a função foi chamada e guardaremos o nó mais distante daquele nó e ao final de tudo retornaremos ele.
> 
> - Agora na função $tree\_diamater$ chamaremos uma $DFS$ para um nó arbitrário e o nó mais distante desse nó arbitrário será utilizado para chamar outra $DFS$, com isso encontraremos o tamanho do diâmetro do grafo.

> [!note]- Complexidade
> $O(V)$, pois o grafo é uma árvore.

```cpp
typedef pair<int, int> pii;

pii dfs(const vector<vector<int>> &g, int curr, int d = 0, int p = -1) {
    pii most_distant {curr, d};

    for (int neigh : g[curr]) {
        if (neigh != p) {
            pii result {dfs(g, neigh, d + 1, curr)};

            if (result.second > most_distant.second) {
                most_distant = result;
            }
        }
    }

    return most_distant;
}

int tree_diameter(const vector<vector<int>> &g) {
	return dfs(g, dfs(g, 0).first).second;
}
```

---