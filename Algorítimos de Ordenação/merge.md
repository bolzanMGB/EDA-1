# Merge Sort

```cpp
void merge_sort(int *v, int l, int r) {
    if (l >= r) return;
    int m = (r + l) / 2;

    merge_sort(v, l, m);
    merge_sort(v, m + 1, r);
    merge(v, l, m, r);
}

```

```cpp
void merge1(int *v, int l, int m, int r) { // intercala
    // l=2 r=8 -> 7 itens = 8+1 -2
    int tam = r + 1 - l;
    int *aux = malloc(sizeof(int) * tam); // espaço auxiliar

    int i = l;     // início do sub-vetor esquerdo
    int j = m + 1; // início do sub-vetor direito
    int k = 0;     // início do vetor auxiliar

    while (i <= m && j <= r) { // percorrer os sub-vetores
        if (v[i] <= v[j])      // testar sub-vetores
            aux[k++] = v[i++]; // ordenar no vetor auxiliar
        else
            aux[k++] = v[j++]; // ordenar no vetor auxiliar
    }

    // ainda tem elementos nos sub-vetores?
    while (i <= m) aux[k++] = v[i++]; // consumir sub-vetor esquerdo
    while (j <= r) aux[k++] = v[j++]; // consumir sub-vetor direito

    // copiar para o vetor original
    for (k = 0, i = l; i <= r; i++, k++) // v[i] e aux[k]
        v[i] = aux[k];                   // copiar o aux[k] para v[i]

    // liberar memória
    free(aux);
}
```
## Passos:
### 1. Dividir em pequenas partes
### 2. Ordenar essas partes
### 3.  Combinar essas partes ordenadas até formar uma única sequência ordenada
