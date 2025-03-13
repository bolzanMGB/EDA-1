
# Selection Short
    
```cpp
void selection_sort(int v[], int l, int r) {
    int menor;

    for (int i = l; i < r; i++) { // n
        menor = i;
        // (n - 1), (n - 2), (n - 3), ..., 0
        // PA ((n + 0) * n) / 2 = (n * n) / 2
        for (int j = i + 1; j <= r; j++) {
            if (v[j] < v[menor]) // (n * n) / 2 comparações
                menor = j;
        }

        if (i != menor)
            exch(v[i], v[menor]); // n trocas
    }
}
```
    
## Passos:
### 1. i : posicionar, j : selecionar, m : índice do menor, l: menor índice do vetor, r: maior índice do vetor.
### 2. “i” começa por “l”;
### 3. “j” começa do termo após “i” e percorre até “r”.
### 4. “j” compara o  “i” com cada termo para achar o “menor” em relação a  “i” (que é marcado com “m”). 
### 5. Quando “j” chega em “r”, “i” troca de lugar com “m”.
### 6. O processo se repete, agora com “i” + 1, até “r”.