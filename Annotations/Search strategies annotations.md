- Em um problema de busca, queremos encontrar uma solução válida para o problema especificado. Cada problema tem um espaço de busca e uma função objetivo.
- Função objetivo: problemas de busca possuem uma meta, uma função que define quando uma solução é valida, ou seja, se $f(x)$ é a função objetivo para o problema $P$, quando $f(x)$ retorna verdadeiro significa que a solução $x$ é valida para o problema $P$.
- Espaço de busca: basicamente é onde estão todas as soluções possíveis para o problema $P$.
- Algoritmos gulosos: tem como estratégia obter o que parece ser melhor em um determinado momento. Entretanto, pode ser que a solução retornada não seja a melhor, mas é uma estratégia mais fácil de ser implementada.
- Força bruta: testa todas as soluções possíveis para um problema.
- Backtracking: algoritmo de força bruta que encontra todas as soluções possíveis para um problema. Porém, quando estamos em um estado que todas as respostas geradas através desse estado não são melhores que a atual podemos parar a recursão, pois os cálculos gerados serão inúteis, esse caso é conhecido como **poda da backtracking**.
- Problemas de otimização: também possuem um espaço de busca, mas a função objetivo é chamada **função fitness** e em vez de retornar verdadeiro ou falso retorna um número. Quando $fitness(x) > fitness(y)$, a solução $x$ é melhor que a solução $y$. Nesse tipo de problema não queremos apenas uma solução válida, mas a solução com o maior ou menor valor de $fitness(x)$ dentro do espaço de busca.

---