> [!info] Objetivo
> - O objetivo da Digit DP é otimizar o processamento de problemas que envolvem dígitos de todos os números de um intervalo $[L, R]$ que costuma ser grande, permitindo resolver tais problemas de forma eficiente através do armazenamento de estados intermediários

> [!note]- Complexidade
> - $O(\text{the product of all the states})$

```cpp
typedef long long ll;

// Below is the skeleton of a simple Digit DP that must be changed depending of the problem
// Remember that lower and upper must have the same number of digits
// If they are different you need to put 0s in lower's left
ll solver(int idx, bool can_low, bool can_high, const string &lower, const string &upper);
```

---
