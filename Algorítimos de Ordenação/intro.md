# Intro Sort

## 1. Características:

- Utiliza as eficiências e evita as deficiências de cada método;
- Insertion: adaptativo;
- Quick: inplace e bom desempenho;
- Merge e heap: previsibilidade de desempenho;
- Quando a recursividade atinge um máximo estipulado, alterna-se para outro método;

## 2. Passos:

- Começa com o Quick: divide o array em partes menores;
    - Com o partion e as recursivas do proprio intro;
- Muda pro Heap: se arecursão do QuickSort atingir uma profundidade maior que **log₂(n) * 2;**
- Insertion: quando os subarrays ficam pequenos (≤ 15 elementos), vem o **InsertionSort** para refinar os dados;

## 3. Inserção:

```cpp
void intro(int *v, int l, int r, int maxdepth) {
    if (r - l <= 15) {
        // insertion_sort(v, l, r);
        return;
    } else if (maxdepth == 0) {
        // merge_sort(v, l, r);
        heap_sort(v, l, r);
    } else {
        compexch(v[l], v[(l + r) / 2]);
        compexch(v[l], v[r]);
        compexch(v[r], v[(l + r) / 2]);

        int p = partition(v, l, r);
        intro(v, l, p - 1, maxdepth - 1);
        intro(v, p + 1, r, maxdepth - 1);
    }
}

void intro_sort(int *v, int l, int r) {
    // proporcional à altura de uma árvore balanceada
    int maxdepth = 2 * ((int)log2((double)(r - l + 1)));

    intro(v, l, r, maxdepth);
    insertion_sort(v, l, r);
}
```

## 4. Decoreba:

- Complexidade no pior caso: n log n;
- in-place: sim;
- Estável: não;
- Adaptativo: não;
