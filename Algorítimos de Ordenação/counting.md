# Counting Sort

## 1. Características:

- É um algoritmo de ordenação **não comparativo;**
- Conta quantas vezes cada número aparece (as frequências de cada chave);
- Funciona bem para ordenar números inteiros em um intervalo conhecido e limitado;
- Contar as frequências de cada chave, calcular as posições através das frequência, Distribuir as chaves;
- Dependende mais do intervalo dos valores do que a quantidade de elementos;

## 2. Passos:

- Encontrar o min e o max do array;
- Criar um array de contagem com tamanho (max + 1);
- Exemplo: v[5] =[ 2 3 3 4 1 ]:
    - Array de contagem: v [6] = 0 1 2 3 4 5 (índices);
- Fase 1: contar as frequencias:
    - v[6] = 0 0 1 1 2 1
        
                  0 1 2 3 4 5
        
- Fase 2: calcular as posições: (somar com as posições anteriores);
    - v[6] = 0 0 1 2 4 5
- Fase 3: distribuvir os elementos:
    - v[6] = 1 2 3 3 5
        
                  0 1 2 3 4
        

## 3. Implementação:

```cpp
#define MAX 10000
#define R 5

int aux[MAX];

void countingsort(int *v, int l, int r) {
    int i, count[R + 1];

    // zerando
    for (i = 0; i <= R; i++) count[i] = 0;

    // frequências
    for (i = l; i <= r; i++) count[v[i] + 1]++;

    // posições
    for (i = 1; i <= R; i++) count[i] += count[i - 1];

    // distribuição
    for (i = l; i <= r; i++) aux[count[v[i]]++] = v[i];

    // cópia: a partir de aux[0]; ex.: i=l=3, i-l=0
    for (i = l; i <= r; i++) v[i] = aux[i - l];
}  
```

## 4. Decoreba:
- Complexidade no pior caso: O(N + R) (numero de chaves(tamanho do array), intervalo de chaves (numero maior mais um))
- in-place: não;
- Estável: sim;
- Adaptativo: não;
- Não comparativo;
