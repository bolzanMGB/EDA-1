# Quick Sort

```cpp
void quick_sort(int *v, int l, int r) {
    // Condição de parada
    if (r <= l) return;

    // Posicionando o pivô
    int p = partition(v, l, r);

    // Ordena os sub-vetores
    quick_sort(v, l, p - 1); // Menores
    quick_sort(v, p + 1, r);  // Maiores
}

```

```cpp
// Sedgewick: pivô à direita
int partition(int *v, int l, int r) {
    int pivot = v[r];  // O pivô é o último elemento
    int i = l - 1, j = r;

    // Enquanto os índices não se cruzarem
    while (i < j) {
        // Procurar elementos maiores que o pivô
        while (v[++i] < pivot) ; // i < r não é necessário aqui, pois i vai até j e j já é garantido que é maior que l
        
        // Procurar elementos menores que o pivô
        while (v[--j] > pivot && j > l) ; // Aqui, j é decrementado, e a condição j > l evita que j vá além da posição l

        // Se o maior está atrás do menor, troca-os
        if (i < j) {
            exch(v[i], v[j]); // Troca os elementos v[i] e v[j]
        }
    }

    // Posiciona o pivô na posição correta (entre os menores e maiores)
    exch(v[i], v[r]); // Coloca o pivô na posição de i

    // Retorna a nova posição do pivô
    return i;
}
```

```cpp
// Sedgewick: pivô à esquerda
int partition(int *v, int l, int r) {
    int pivot = v[l];    // O pivô é o primeiro elemento
    int i = l;           // Inicializa i com o índice l (ponto de partida)
    int j = r + 1;       // Inicializa j com o índice r+1 (ponto além do último elemento)

    while (i < j) {
        // Procurar elementos maiores que o pivô
        while (v[++i] < pivot && i < r) ; // Incrementa i até encontrar um elemento maior que o pivô

        // Procurar elementos menores que o pivô
        while (pivot < v[--j] && j > l) ; // Decrementa j até encontrar um elemento menor que o pivô

        // Se os elementos em i e j estão na ordem errada, troca-os
        if (i < j)
            exch(v[i], v[j]);  // Troca v[i] com v[j]
    }

    // Posiciona o pivô na posição correta, antes do primeiro elemento maior
    exch(v[l], v[j]);  // Coloca o pivô na posição j

    return j;  // Retorna a posição do pivô
}
```

## Decisão de projeto:
### 1. Pivô: elemento mais a esquerda ou mais a direita;
### 2. i (procura elemento maior): E → D;
### 3. j (Procurar emento menor): D → E;
### 4. Condição de parada: i e j se encontram;
    
## Passos:
### 1. Primeiro o i, depois o j. Anda um elemento por vez;
### 2. i vai da esquerda para direita, se achar um elemento maior que o pivô para;
### 3. j vai da direita para esquerda, se achar um elemento maior que o pivô para;
### 4. Troca i com j;
### 5. Quando i e j se encontram: pivô vai para aquele lugar;
### 6. Ocorre divisão em sub-vetores (esquerda e direita em relação ao pivô;
### 7. Novo pivô é selecionado; 
    
## Otimação da mediana: 
### 1. Escolhe o pivô de forma mais eficiente;
### 2. O pivô é escolhido entre três elementos: o primeiro, o último e o do meio da lista;