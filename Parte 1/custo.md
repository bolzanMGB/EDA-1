Custo

1. Constante (c)

Instruções são realizadas um número fixo de vezes independente do tamanho.

1.1 Exemplos:

Listas estáticas: acesso a índices; inserção;

Listas duplamente encadeadas: remoção de nós; inserção após um nó; inserção antes de um nó;

int operacao(int n, int a, char op) {
    int r = 0; // atribuição
    if (op == '+')
        r = n + a; // comparação
    else if (op == '-')
        r = n - a; // comparação
    else if (op == '*')
        r = n * a; // comparação + aritmética + atribuição
    
    return r;
}

2. Linear

Cresce a uma taxa constante de acordo com o aumento da entrada. Percorre cada elemento.

2.1 Exemplos:

Busca sequencial;

Listas simplesmente encadeadas: remoção de um nó específico e inserção antes de um nó específico;

Fatorial por recorrência;

int pesquisa(int x, int n, int v[]) {
    for (int i = 0; i < n && v[i] != x; i = i + 1);
    return i;
}

3. Quadrática

Cresce proporcionalmente ao quadrado do tamanho da entrada.

void ordenacao(int v[], int n) {
    for (int i = 1; i < n; i++) { // a partir do segundo elemento
        for (int j = i; j > 0 && v[j] < v[j - 1]; j--) { // comparar com os antecessores
            troca(v[j], v[j - 1]); // posicionar
        }
    }
}

4. Cúbica

Cresce proporcionalmente ao cubo do tamanho da entrada.

void multiplica_matrizes(int A[3][3], int B[3][3], int C[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            C[i][j] = 0;
            for (int k = 0; k < 3; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
    imprime_matriz(C);
}

5. Exponencial (K^n)

n múltiplas sucessivas de uma base (número fixo de chamadas recursivas).

int p(int n) {
    if (n == 0) return 0;
    else if (n == 1) return 1;
    return p(n - 1) + p(n - 2);
}

6. Fatorial

Cada chamada executa múltiplas (linear) chamadas recursivas.

void anagram(char str[], int k) {
    char tmp;
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

void subsets(int v[], int i, int n, int sub[], int fim) {
    for (int j = 0; j < fim; j++)
        printf("%d ", sub[j]);
    printf("\n");

    for (; i < n; i++) {
        sub[fim] = v[i];
        subsets(v, i + 1, n, sub, fim + 1);
    }
}

7. Logarítmica

7.1 Características:

É a inversa da função exponencial;

Fica um pouco mais lento à medida que n cresce;

A solução do problema concentra-se na solução de subproblemas;

Muito rápido para grandes entradas;

Busca binária;

int pesquisa(int x, int v[], int esq, int dir) {
    int meio = (esq + dir) / 2;
    if (v[meio] == x) return meio;
    if (esq >= dir) return -1;
    else if (v[meio] < x)
        return pesquisa(x, v, meio + 1, dir);
    else
        return pesquisa(x, v, esq, meio - 1);
}

8. Linearítimo

8.1 Características:

Divisão e conquista: quebrando o problema em problemas menores, resolvendo cada um deles independentemente e depois juntando as soluções, localmente resolvidos, gerando uma nova solução;

Percorre cada elemento, enquanto quebra;

Merge Sort;

