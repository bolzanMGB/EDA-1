# Tipos de Complexidade de Custo de Algoritmos


## 1. Constante (O(1))
- Instruções são realizadas um número fixo de vezes, independentemente do tamanho da entrada.

### Exemplos:
- Listas estáticas: acesso a índices; inserção;
- Listas duplamente encadeadas: remoção de nós; inserção após um nó; inserção antes de um nó;

```c
int operacao(int n, int a, char op) {
    int r = 0; // atribuição
    if (op == '+')
        r = n + a;
    else if (op == '-')
        r = n - a;
    else if (op == '*')
        r = n * a;
    return r;
}
```

---

## 2. Linear (O(n))
- Cresce a uma taxa constante de acordo com o aumento da entrada.
- Percorre cada elemento.

### Exemplos:
- Busca sequencial;
- Listas simplesmente encadeadas: remoção de um nó específico e inserção antes de um nó específico;
- Fatorial por recorrência;

```c
int pesquisa(int x, int n, int v[]) {
    for (int i = 0; i < n && v[i] != x; i++);
    return i;
}
```

---

## 3. Quadrática (O(n^2))
- Cresce proporcionalmente ao quadrado do tamanho da entrada.

```c
void ordenacao(int v[], int n) {
    for (int i = 1; i < n; i++) {
        for (int j = i; j > 0 && v[j] < v[j - 1]; j--) {
            troca(v[j], v[j - 1]);
        }
    }
}
```

---

## 4. Cúbica (O(n^3))
- Cresce proporcionalmente ao cubo do tamanho da entrada.

```c
void multiplica_matrizes(int A[3][3], int B[3][3], int C[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            C[i][j] = 0;
            for (int k = 0; k < 3; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}
```

---

## 5. Exponencial (O(K^n))
- Múltiplas sucessivas chamadas recursivas.

```c
int p(int n) {
    if (n == 0) return 0;
    else if (n == 1) return 1;
    return p(n - 1) + p(n - 2);
}
```

---

## 6. Fatorial (O(n!))
- Cada chamada executa múltiplas chamadas recursivas.

```c
void anagram(char str[], int k) {
    int i, len = strlen(str);
    if (k == len)
        printf("%s\n", str);
    else {
        for (i = k; i < len; i++) {
            swap_char(str, k, i);
            anagram(str, k + 1);
            swap_char(str, i, k);
        }
    }
}
```

---

## 7. Logarítmica (O(log n))
#### Características:
- Inversa da função exponencial;
- Fica um pouco mais lento à medida que n cresce;
- Muito rápido para grandes entradas.

### Exemplos:
- Busca binária;

```c
int pesquisa(int x, int v[], int esq, int dir) {
    int meio = (esq + dir) / 2;
    if (v[meio] == x) return meio;
    if (esq >= dir) return -1;
    else if (v[meio] < x)
        return pesquisa(x, v, meio + 1, dir);
    else
        return pesquisa(x, v, esq, meio - 1);
}
```

---

## 8. Linearítimo (O(n log n))
### Características:
- Utiliza o paradigma de Divisão e Conquista;
- Divide o problema em subproblemas menores;
- Muito eficiente para grandes entradas.

### Exemplos:
- Merge Sort;

```c
void merge_sort(int v[], int inicio, int fim) {
    if (inicio < fim) {
        int meio = (inicio + fim) / 2;
        merge_sort(v, inicio, meio);
        merge_sort(v, meio + 1, fim);
        merge(v, inicio, meio, fim);
    }
}
```

