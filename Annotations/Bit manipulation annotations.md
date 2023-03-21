## AND (&)

- O AND bitwise é um operador binário que recebe dois bits e emite um outro de tal forma que o bit retornado só é **true** se e somente se ambos os bits forem **true**.

## OR (|)

- O OR bitwise é um operador binário que recebe dois bits e emite um outro de tal forma que o bit retornado só é **true** se um dos bits for **true**.

## XOR (^)

- O XOR bitwise é um operador binário que recebe dois números e emite um outro de tal forma que o bit retornado só é **true** se os seus bits forem diferentes.

## Left shift (<<) e Right shift (>>)

- Ambos os operadores bitwise trabalham de uma forma muito semelhante. Ambos recebem um número $x$ e um número $k$ e devolvem o valor de $x$ com seus bits deslocados $k$ vezes para a esquerda (left shift) ou $k$ vezes para a direita (right shift). Vale notar que realizar um left shift em um número $x$ é o mesmo que multiplicá-lo por $2^k$ e aplicar o right shift é o mesmo que realizar uma divisão inteira por $2^k$.

## NOT (~)

- Retorna o complemento de 1 de um número. Porém, vale lembrar que números negativos são representados utilizando complemento de 2.

## Truques úteis usando manipulação de bits

- Checar se o bit na posição $k$ está ativo

```cpp
bool is_set(int x, int k) {
    return (x & (1 << k)) != 0;
}
```

- Acender um bit de um número na posição $k$

```cpp
bool set_bit(int &x, int k) {
    x |= (1 << k);
}
```

- Apagar um bit de um número na posição $k$

```cpp
bool set_bit_off(int &x, int k) {
    x &= ~(1 << k);
}
```

- Checar se um número é uma potência de dois

```cpp
bool is_power_of_two(int x) {
    return (x & (x - 1)) == 0;
}
```

- Bit menos significativo

```cpp
bool lsb(int x) {
    return x & -x;
}
```

## Máscara de bits

- Uma máscara de bits é a representação de um subconjunto feita a partir da representação binária de um número. Os métodos a seguir podem ser utilizados nela.

### Checar se um conjunto é subconjunto de outro conjunto

```cpp
bool is_submask(int a, int b) {
    return (a & b) == a;
}
```

### Iterar por todas as submascaras de um número

```cpp
void iterate_through_submasks(int x) {
    for (int i {x}; i > 0; i = (i - 1) & x) {
        // do something
    }
}
```

### Iterar por todas as máscaras e suas sub-máscaras

```cpp
void iterate_through_all_submasks(int x) {
    for (int mask {}; mask < (1 << n); ++mask) {
        iterate_through_submasks(mask);
    }
}
```

---