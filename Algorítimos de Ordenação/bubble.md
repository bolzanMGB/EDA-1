# Bubble Short
    
```cpp
void bubble_sort(int v[], int l, int r) {
    int swap = 1;
    while (r > l && swap) { //n
        swap = 0;
        for (int j = l; j < r; j++) {
            // comparações
            //(n -1), (n -2), (n -3), ..., 0
            if (v[j] > v[j + 1]) {
                // trocas
                //(n -1), (n -2), (n -3), ..., 0
                exch(v[j], v[j + 1]);
                swap = 1;
            }
        }
        r--;
    }
    //f(n) = (n*n)/2 + (n*n)/2
}
```
    
## Passos:
### 1. j : selecionar, l: menor índice do vetor, r: maior índice do vetor.
### 2. “j” vai percorrer o vetor de “l” até “r”.
### 3. Caso o índice “j” for maior que o índice “j” + 1, ocorre um swap.
### 4. Ao percorrer o vetor inteiro, o processo recomeça.
### 5. Caso houver nenhum swap, o vetor vai estar ordenado.