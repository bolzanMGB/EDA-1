# Estruturas de Busca

## 1) Busca Sequencial
A busca sequencial percorre cada elemento da estrutura de dados até encontrar o elemento desejado ou chegar ao final da lista.

### 1.1 Complexidade
- **Melhor caso:** O(1) → Quando o elemento está na primeira posição.
- **Caso médio:** O(n) → Em média, verifica metade dos elementos.
- **Pior caso:** O(n) → Quando o elemento está na última posição ou não está presente.

### 1.2 Complexidade por Estrutura
- **Listas Encadeadas:**
  - Inserção e remoção: O(1).
  - Busca: O(n).
- **Vetores Não Ordenados:**
  - Busca: O(n).
  - Inserção e remoção: O(1).
- **Vetores Ordenados:**
  - Busca: O(n).
  - Inserção e remoção: O(n).

---

## 2) Busca Binária
A busca binária é um método eficiente para encontrar um elemento em um vetor ordenado, reduzindo o espaço de busca pela metade a cada iteração.

### 2.1 Implementação em C++
```cpp
#define key(A) (A.chave)

typedef int Key;
typedef struct data Item;
struct data { 
    Key chave; 
    char info[100]; 
};

int binary_search(Item *v, int l, int r, Key k) {
    // condição de parada
    if (l > r) return -1;

    // calcular o índice central
    int m = (l + r) / 2; // l + (r - l) / 2

    // comparar k com o elemento central
    if (k == key(v[m])) return m;

    // procurar à esquerda
    if (k < key(v[m]))
        return binary_search(v, l, m - 1, k);

    // procurar à direita
    return binary_search(v, m + 1, r, k);
}
```

### 2.2 Exemplo
Se tivermos um vetor ordenado:

```
V[10] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
Índices =  0  1  2  3  4  5  6  7  8  9
```

Buscando o número `7`:

1. Calcular o meio: `(9 - 0) / 2 + 0 = 4`
2. Comparar `V[4]` com `7` → Como `V[4] < 7`, buscamos à direita.
3. Novo meio: `(9 - 5) / 2 + 5 = 7`
4. Comparar `V[7]` com `7` → Como `V[7] > 7`, buscamos à esquerda.
5. Novo meio: `(6 - 5) / 2 + 5 = 6`
6. Encontramos `V[6] = 7`, retornamos a posição `6`.

### 2.3 Complexidade
A complexidade da busca binária é **O(log₂ n)**, pois a cada iteração reduzimos o espaço de busca pela metade.

---

Esse documento apresenta as operações fundamentais de busca e suas complexidades para diferentes estruturas de dados.

