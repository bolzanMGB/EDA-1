# Heap Sort

## 1. Passos:

- Fase 1:
    - Transformar a lista original em um heap máximo;
    - Começa pela metade do array;
    - Concerta até chegar na raiz;
- Fase 2:
    - Trocar a raiz pelo ultimo elemento;
    - Remover raiz;
    - Diminuir tamanho da fila;
    - fixDown;
    - loop;

## 2. Inserção:

```cpp

// Definição do tipo Item (ajuste conforme necessário)
typedef int Item;

// Função para trocar dois elementos
void exch(Item *a, Item *b) {
    Item temp = *a;
    *a = *b;
    *b = temp;
}

// Função para restaurar a propriedade de heap (max-heap)
void fixDown(Item *pq, int k, int N) {
    while (2 * k <= N) {
        int j = 2 * k; // Filho esquerdo
        if (j < N && pq[j] < pq[j + 1]) j++; // Escolhe o maior filho
        if (pq[k] >= pq[j]) break; // Se o pai é maior que o filho, para
        exch(&pq[k], &pq[j]); // Troca pai e filho
        k = j; // Continua no filho
    }
}

// Função principal do Heap Sort
void heap_sort(Item *v, int l, int r) {
    Item *pq = v + l - 1; // Ajusta o ponteiro para o heap
    int N = r - l + 1;    // Tamanho do heap

    // Constrói o heap (max-heap) // primeira fase
    for (int k = N / 2; k >= 1; k--) {
        fixDown(pq, k, N);
    }

    // Ordena o array // segunda fase
    while (N > 1) {
        exch(&pq[1], &pq[N]); // Troca o maior elemento (raiz) com o último
        fixDown(pq, 1, --N);  // Restaura a propriedade de heap
    }
}
```

## 3. Decoreba:

- Complexidade: n log n;
    - fixDown: n;
    - insertion: log n (remover raiz);
- In-place: sim;
- Estabilidade: não;
- Adaptatividade: não;

