## Trigonometria

### Seno, cosseno e tangente

- Considere um triângulo retângulo com catetos $a$ e $b$, hipotenusa $c$ e um ângulo $\alpha$. Dizemos que $a$ é o cateto oposto a $\alpha$ e o cateto $b$ é o cateto adjacente.

![[Triângulo retângulo.png | center | 170]]
- Existem três funções que relacionam $a, b, c \text{ e } \alpha$:
	1. Seno(sin): $\sin \alpha = \dfrac{\text{cateto oposto}}{hipotenusa} = \dfrac{a}{c}$
	2. Cosseno(cos): $\cos \alpha = \dfrac{\text{cateto adjacente}}{hipotenusa} = \dfrac{b}{c}$
	3. Tangente(tan): $\tan \alpha = \dfrac{\text{cateto oposto}}{\text{cateto adjacente}} = \dfrac{a}{b}$


### Círculo trigonométrico

![[Círculo trigonométrico.png | center | 170]]

- O círculo trigonométrico é apenas uma circunferência com raio de tamanho 1 centrado na origem. Ao calcular o $\sin \alpha = \dfrac{y}{r} = y$ e $\cos \alpha = \dfrac{x}{r} = x$. Portanto, o ponto $(x, y)$ é igual a $(\sin \alpha, \cos \alpha)$. Já a $\tan \alpha = \dfrac{\sin \alpha}{\cos \alpha}$.

### Radianos e graus

- A forma mais comum de medir os ângulos é em graus. Mas há outra unidade conhecida como radianos (rad). Para converter graus para radianos é só utilizar uma regra de três $\dfrac{2 \cdot \pi \cdot r}{x} = \dfrac{360\degree}{y}$, no qual $x$ está em radianos e $y$ em graus.

### Identidades trigonométricas

- Considere que $\theta$ é qualquer ângulo e $ABC$ é o seguinte triângulo:

![[Identidades trigonométricas.png | center | 170]]

- As três entidades trigonométricas mais comuns são:
	1. Relação trigonométrica fundamental: $\sin^2 \theta + \cos^2 \theta = 1$
	2. Lei dos senos: $\dfrac{a}{sin \alpha} = \dfrac{b}{sin \beta} = \dfrac{c}{sin \gamma}$
	3. Lei dos cossenos: $a^2 = b^2 + c^2 - 2 \cdot b \cdot c \cdot \cos \alpha$

---

## Geometria vetorial

- Um vetor $\vec{v}$ nada mais é do que uma seta em um plano. Ele tem três propriedades:
		1. Magnitude
		2. Direção
		3. Sentido

### Operação com vetores

- Soma de vetores: considere um vetor $\vec{v}$ tal que $\vec{v} = \vec{a} + \vec{b}$, isso significa que as coordenadas de $\vec{v}$ são $(x_a + x_b, y_a + y_b)$.
- Oposto de um vetor: o oposto de um vetor $\vec{v}$ é dado por $-\vec{v}$, as coordenadas de $-\vec{v}$ são $(-x_v, -y_v)$.
- Diferença de vetores: considere um vetor $\vec{v}$ tal que $\vec{v} = \vec{a} - \vec{b}$, isso significa que as coordenadas de $\vec{v}$ são dadas pela soma de $\vec{a} + (-\vec{b})$, ou seja, $\vec{v} = (x_a - x_b, y_a - y_b)$.
- Multiplicação de um vetor por um escalar: considere um vetor $\vec{v}$ tal que $\vec{v} = \vec{a} \cdot k$, onde $k$ é um escalar. Se $k > 0$, então $\vec{v}$ é um vetor com o mesmo sentido e direção de $\vec{a}$, mas com seu comprimento $k$ vezes maior que $\vec{a}$. Se $k < 0$, então $\vec{v}$ é um vetor com a mesma direção e sentido oposto de $\vec{a}$, mas com o comrpimento $-k$ vezes maior que $\vec{a}$. Para obter $\vec{v}$ após a multiplicação de $\vec{a} \cdot k$, basta fazer $\vec{v} = (k \cdot x_a, k \cdot y_a)$.
- Igualdade: podemos dizer que um vetor $\vec{a}$ é igual a um vetor $\vec{b}$ se sua magnitude, direção e sentido forem iguais.
- Produto escalar (dot product): considere um vetor $\vec{a}$ e um vetor $\vec{b}$, o produto escalar entre os dois é dado por $||\vec{a}|| \cdot ||\vec{b}|| \cdot \cos \theta$. Já a definição algébrica do produto escalar é dado por $a_x \cdot b_x + a_y \cdot b_y$. Algumas propriedades do produto escalar, são:
	1. Tamanho ao quadrado (norm): $||\vec{a}||^2 = \vec{a} \cdot \vec{a}$
	1. Tamanho de $\vec{a}$: $||\vec{a}|| = \sqrt{\vec{a} \cdot \vec{a}}$ ou $||\vec{v}|| = \sqrt{x^2 + y^2}$
	2. Projeção de $\vec{a}$ em $\vec{b}$: $\dfrac{\vec{a} \cdot \vec{b}}{||\vec{b}||}$
	3. Ângulo entre dois vetores: $\arccos (\dfrac{a \cdot b}{||\vec{a} \cdot \vec{b}||})$
- Produto vetorial (cross product): considere um vetor $\vec{a}$ e um vetor $\vec{b}$, o produto vetorial entre os dois é dado por $||\vec{a}|| \cdot ||\vec{b}|| \cdot \sin \theta$. Para planos eu posso dizer que $\vec{a} \times \vec{b} = a_x \cdot b_y - a_y \cdot b_x$.

### Outras definições com vetores

- Ângulo entre vetores: considere dois vetores $\vec{a}$ e $\vec{b}$, o ângulo entre esses vetores é o ângulo entre as duas setas no plano. Para evitar ambiguidades, dizemos que é o ângulo de um vetor para o outro no sentido horário ou anti-horário.
- Vetor entre dois pontos: considere dois pontos $A$ e $B$, se quisermos saber as coordenadas de um vetor que começa em $A$ e termina em $B$, temos que $\vec{a} = (x_A, y_A)$ e $\vec{b} = (x_B, y_B)$, o vetor $\vec{AB} = \vec{a} - \vec{b}$.

---