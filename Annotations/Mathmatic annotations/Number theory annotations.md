- Esta subárea da matemática estuda os números inteiros e as suas propriedades.

---

## Divisores e múltiplos

- considere dois inteiros $a, b$ tal que $b \vert a$, ou seja, o resto da divisão de $a$ por $b$ é 0. Neste caso, podemos dizer que $b$ é um divisor de $a$ ou $a$ é um múltiplo de $b$. Para dizer que $b$ não é um divisor de $a$ podemos utilizar a seguinte notação: $b \nmid a$.

---

## Números primos e compostos

- Um número é chamado primo se e somente se ele tiver exatamente 2 divisores positivos e um número é chamado composto se e somente se ele tem mais do que 2 divisores positivos. Vale notar que o número 1 é o único número que não se encaixa em nenhuma das duas definições, por tanto, ele é o único número inteiro positivo que não é primo e nem é composto.

---

## Fator primo e fatoração prima

- Um primo $P$ é chamado fator primo de um número inteiro $x$ se e somente se $p \vert x$. A partir dessa definição vem o conceito de fatoração prima: a fatoração prima de um inteiro $x$ é a decomposição de $x$ em um produto de alguns primos.

---

## Aritmética Modular

- A operação de módulo pode ser definida utilizando o perador $mod$. Dados $a, b \text{ | } b \neq 0, a \text{ mod } b$ é igual ao resto da divisão de $a$ por $b$. Com isso, pode-se extrair uma fórmula simples, mas muito útil da sua definição: $a = \lfloor \dfrac{a}{b} \rfloor b + a \text{ mod } b$ que é baseada na divisão euclidiana de $a$ por $b$.
- A respeito de congruências, dados três inteiros $a, b, n$, dizemos que $a \equiv b \text{ (mod n)}$ se e somente se $a \text{ mod n}= b \text{ mod n}$, neste caso, podemos dizer que $a$ é congruente a $b$ módulo $n$. Esta relação tem muitas propriedades, algumas são:
    1. $a \equiv a \text{ (mod n)}$
    2. $a \equiv b \text{ (mod n)} \leftrightarrow b \equiv a \text{ (mod n)}$
    3. $a \equiv b \text{ (mod n)}$ e $b \equiv c \text{ (mod n)}$, então $a \equiv c \text{ (mod n)}$
    4. $a \equiv a + kn \text{ (mod n)}$, para qualquer inteiro $k$

### Inverso modular

- Na aritmética modular, podemos facilmente lidar com adições, substrações e multiplicações, mas não quando se trata de divisões, porque quando dividimos um número inteiro por outro, o resultado não será necessariamente um número inteiro. Devido a esse problema, que o inverso modular foi criado. Dizemos que $x$ é o inverso modular de $a \text{ mod } m$ se e somente se $ax \equiv m$ e $0 \leq x < m$. Entretanto há números que não possuem inverso modular módulo $m$. Existem duas propriedades interessantes dos inversos modulares:
	1. Um inteiro $a$ tem um inverso modular módulo $m$ se $mdc(a, m) = 1$.
	2. Para cada inteiro $a$, ele tem no máximo um inverso modular módulo $m$.
- Como o inverso modular de um número módulo $m$ é único, podemos reprensentá-lo por $a^{-1}$.

---

## Indução matemática

- A indução matemática é uma técnica de prova. Considerando que queremos provar uma declaração para cada número $n$, a ideia da indução é quebrar a prova em três passos.

### Indução fraca

- Caso base: prove a declaração para casos pequenos.
- Hipótese: suponha que a afirmação é verdadeira para um número inteiro $n$.
- Passo indutivo: prove que a declaração é verdadeira para $n + 1$.

### Indução forte

- Caso base: prove a afirmação para casos pequenos.
- Hipótese: suponha que a declaração é verdadeira para qualquer número inteiro menor que $n$.
- Passo indutivo: prove que a declaração é verdadeira para $n$.

---