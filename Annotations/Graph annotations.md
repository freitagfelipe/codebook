## Definições

- Grafos bidirecionais: aqueles que as arestas são mão dupla.
- Grafos direcionados: aqueles que as arestas possuem apenas um sentido de direção.
- Grafo completo: aquele que para todos os vértices $v, u \in V$ existe uma aresta ligando $u$ a $v$.
- Sub-grafo: um grafo $G' = (V', E')$ é dito um _sub-grafo_ de $G = (V, E)$ se, e somente se, $V' \subset V \text{ e } E' \subset E$.
- Conexidade: um grafo é dito conexo se para todos os vértices $u, v \in V$ existir um caminho de um para o outro.
- Componente conexa: é um conjunto (máximo) de vértices tal que o sub-grafo gerado por eles é conexo.
- Componente fortemente conexa: semelhante a componente conexa, porém para grafos direcionados. Nesse caso para todos os vértices $u, v \in V$ é necessário não só que $(u, v) \in E$, mas também que $(v, u) \in E$.
- Ciclo: um grafo possui um ciclo quando existe um caminho de um vértice a si mesmo e sem repetir arestas.
- Árvore: um grafo bidirecional é chamado de árvore se, e somente se, ele for conexo e não tiver ciclos.
- Floresta: um grafo que não contém ciclos mas que também não é conexo pode ser visto como um conjunto de árvores.
- Grafo denso: um grafo é dito denso se a quantidade de arestas é aproximadamente o número de vértices ao quadrado.

---

## Representação de um grafo

- Lista de arestas.
- Matriz de adjacência.
- Lista de adjacência.

---

## Busca em grafos

- DFS (depth-first-search): se trata de, em cada passo, olhar os vizinhos do nó atual que se está avaliando e, para cada um deles cuja componente ainda não foi determinada, fazer sua componente conexa ser a mesma do nó atual e chamar a função recursivamente nele.
- BFS (breadth-first-search): se trata de fazer o mesmo procedimento da DFS. Porém, em vez de chamar a função recursivamente em um vizinho, esté é adicionado a uma fila e processado posteriormente.

---