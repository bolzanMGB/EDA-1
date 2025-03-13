# Radix Sort

## 1. Características:

- Comparar a estrutura das chaves (linear);
- Útil para ordenar números inteiros grandes e strings;
- Decompõe a chave em partes menores (como dígitos ou bytes) e ordena os elementos com base nessas partes;
- Para números, ele pode ordenar com base nos dígitos (unidades, dezenas, centenas, etc.);
- Quando W é pequeno e fixo, Radix Sort pode ser mais rápido que algoritmos baseados em comparação (O(N log N))
- Usa o counting sort;

## 2. Passos:

- Começa ordenando os números pelo dígito menos significativo e move-se para o próximo dígito à esquerda até todos serem processados;
- Para cada dígito, o Radix Sort utiliza um algoritmo de ordenação estável, como **Counting Sort**, para ordenar os números com base no dígito atual.

## 3. Tipos:

### 3.1 LSD (Least Signicant Digit)

- Direita para a esquerda;
- Strings de tamanho fixo pequenas;
- Complexidade: W ∗ N (tamanho da chave, numero de chaves);

```cpp
# define bytesword 4 // int
# define bitsbyte 8

# define R (1 << bitsbyte )
# define digit (N , D ) ((( N ) >> (( D ) * bitsbyte ) ) & (R -1) )
void radix_sortLSD(int *v, int l, int r) {
    int i, w, k;
    int aux[r - l + 1], count[R + 1];

    // byte w
    for (w = 0; w < bytesword; w++) {
        memset(count, 0, sizeof(int) * (R + 1));

        // frequências
        for (i = l; i <= r; i++) count[digit(v[i], w) + 1]++;

        // posições
        for (k = 1; k < R; k++) count[k] += count[k - 1];

        // distribuição
        for (i = l; i <= r; i++) aux[count[digit(v[i], w)]++] = v[i];

        // copiando
        for (i = l; i <= r; i++) v[i] = aux[i - l];
    }
}

Lista inicial:          170, 045, 075, 090, 802, 024, 002, 066
Ordenação pela unidade: 802, 002, 024, 045, 066, 170, 075, 090
Ordenação pela dezena:  002, 024, 045, 066, 075, 090, 170, 802
Ordenação pela centena: 002, 024, 045, 066, 075, 090, 170, 802 (lista ordenada)

```

### 3.2 MSD (Most Signicant Digit)

- Esquerda para a direita;
- Tipo de tamanho variavel;
- Ordena-se por subconjuntos
- Complexidade: W ∗ N (tamanho da chave, numero de chaves);

```cpp
// Strings: ordena para o d-ésimo caractere
void radixMSD(char a[][maxstring], int l, int r, int d) {
    if (r <= l) return;

    char aux[r - l + 1][maxstring];
    int count[R + 1];
    memset(count, 0, sizeof(int) * (R + 1));

    // frequências
    for (int i = l; i <= r; i++) count[a[i][d] + 1]++;

    // posições
    for (int i = 1; i < R; i++) count[i] += count[i - 1];

    // distribuição e cópia
    for (int i = l; i <= r; i++) strcpy(aux[count[a[i][d]]++], a[i]);
    for (int i = l; i <= r; i++) strcpy(a[i], aux[i - l]);

    // subconjuntos
    for (int i = 1; i < R; i++)
        radixMSD(a, l + count[i - 1], l + count[i] - 1, d + 1);
}

Lista inicial:     aab,  bba,  aaa,  baaa
Ordenação parcial: [aab, aaa]  [bba, baaa]
Ordenação final:   [aaa] [aab] [bba] [baaa]
```

## 4. Decoreba:

### 4.1 LSD:

- Complexidade no pior, medio, melhor caso: O(w + n)
- in-place: não;
- Estável: sim;
- Adaptativo: não;
- Não comparativo;
- Strings pequenas fixas;

### 4.2 MSD:

- Complexidade no pior caso: O(N + R)
- in-place: não;
- Estável: não;
- Adaptativo: não;
- Não comparativo;
- Strings de tamanho diferente;
