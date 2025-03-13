# Insertion Short (Não Otimizado)

```cpp
void insertion_sort(int v[], int l, int r) {
    // Percorrer o array a partir do segundo elemento
    for (int i = l + 1; i <= r; i++) {
        // Procurar antecessores menores que v[i]
        for (int j = i; j > l && v[j] < v[j - 1]; j--) {
            // Inserir na posição
            exch(v[j], v[j - 1]);
        }
    }
}
```
    
## Passos:
### 1. i : posição inicial, j : selecionar, l: menor índice do vetor, r: maior índice do vetor.
### 2. “i” começa como o segundo índice do vetor e vai percorrer até chegar em “r”.
### 3. “j” é igual o “i”
### 4. São feitas comparações entre “j” e “j - 1”.
### 5. Se encontrar um índice onde “j” é menor, ocorre um swap e “j” volta um índice atrás.
### 6. Caso não houver, “i” avança um indíce para frente.
---
# Insertion Short (Otimizado)

    ```cpp
    	void insertion_sort(int v[], int l, int r) {
        int elem, i, j;
    
        // Percorrer o array a partir do segundo elemento
        for (i = l + 1; i <= r; i++) {
            // Elemento que será (re) inserido
            elem = v[i];
    
            // Para cada elemento maior
            for (j = i; j > l && elem < v[j - 1]; j--) {
                // "Puxar" o maior elemento
                v[j] = v[j - 1];
            }
    
            // Inserir o elemento na sua posição
            v[j] = elem;
        }
    }
    ```
    
## Diferença: 
- não faz uma troca direta, apenas move o numero maior para a direita até chegar ao “j” = 1 ou achar um numero menor que “elem”.