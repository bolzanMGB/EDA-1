# Tipos de Listas 

## 1) Listas Estáticas (Arrays)
- Espaço consecutivo na memória RAM.
- Acesso fácil através de um índice.
- O nome do array corresponde ao endereço de memória.
- **Vantagem:** fácil acesso.
- **Desvantagem:** difícil manipulação (remover, adicionar, modificar).

---

## 2) Listas Simplesmente Encadeadas
É uma sequência de células onde cada célula contém o endereço da célula seguinte. Essa sequência termina na última célula, que contém o valor `NULL` no ponteiro para a próxima célula. O endereço de uma lista encadeada é o endereço de sua primeira célula.

### 2.1 Estrutura
Cada célula contém o conteúdo e o ponteiro para a próxima célula.

```cpp
struct node {
    int conteudo; // Conteúdo da célula
    struct node *ponteiroProximoNode; // Ponteiro para a próxima célula
};

// Alternativas para definição
typedef struct node no;

struct node {
    int conteudo;
    no *ponteiroProximoNode;
};

typedef struct node {
    int conteudo;
    struct node *ponteiroProximoNode;
} no;
```

### 2.2 Cabeça de Lista
Quando a primeira célula da lista é um mero marcador de início e ignora o conteúdo da célula.

```cpp
typedef struct head {
    int num_itens;
    no *prox;
    no *ultimo;
} cabeca;
```

---

### 2.3 Inserir um item no início (após a cabeça)
```cpp
void inserir_inicio(cabeca *cabeça, no *elem) {
    elem->prox = cabeça->prox;
    cabeça->prox = elem;
    cabeça->num_itens++;
    if (elem->prox == NULL) cabeça->ultimo = elem;
}
```

---

### 2.4 Inserir um item após um nó
```cpp
void inserir_depois(cabeca *cabeça, no *ref, no *elem) {
    elem->prox = ref->prox;
    ref->prox = elem;
    cabeça->num_itens++;
    if (elem->prox == NULL) cabeça->ultimo = elem;
}
```

---

### 2.5 Inserir no fim
```cpp
void inserir_fim(cabeca *cabeça, no *elem) {
    if (cabeça->prox == NULL)
        cabeça->prox = elem;
    else
        cabeça->ultimo->prox = elem;
    
    cabeça->ultimo = elem;
    elem->prox = NULL;
    cabeça->num_itens++;
}
```

---

### 2.6 Remover início
```cpp
void remover_inicio(cabeca *lista) {
    if (lista->prox == NULL) return;
    no *lixo = lista->prox;
    lista->prox = lixo->prox;
    lista->num_itens--;
    if (lista->prox == NULL) lista->ultimo = NULL;
}
```

---

### 2.7 Remover qualquer nó
```cpp
void remover_no(cabeca *cabeça, no *lixo) {
    if (cabeça->prox == lixo) {
        cabeça->prox = lixo->prox;
    } else {
        no *ant;
        for (ant = cabeça->prox; ant != NULL && ant->prox != lixo; ant = ant->prox);
        if (ant) {
            ant->prox = lixo->prox;
            cabeça->num_itens--;
            if (ant->prox == NULL) cabeça->ultimo = ant;
        }
    }
}
```

---

### 2.8 Printar o conteúdo de todas as células
```cpp
void imprime(no *le) {
    no *p;
    for (p = le; p != NULL; p = p->prox)
        printf("%d\n", p->conteudo);
}
```

---

### 2.9 Buscar um item
```cpp
no *busca(int x, no *le) {
    no *p = le;
    while (p != NULL && p->conteudo != x) {
        p = p->prox;
    }
    return p;
}
```

---

## 3) Listas Duplamente Encadeadas
- Cada nó armazena o endereço do nó anterior e do próximo.
- Útil para inserções e remoções frequentes, principalmente de elementos intermediários.
- O primeiro nó tem `ant = NULL` e o último nó tem `prox = NULL`.

```cpp
typedef struct node {
    int info;
    struct node *ant;
    struct node *prox;
} no;

typedef struct head {
    int tam;
    no *prox;
    no *ultimo;
} cabeca;
```

---

### 3.1 Inserir depois da cabeça
```cpp
void inserir_inicio(cabeca *lista, no *elem) {
    elem->ant = NULL;
    elem->prox = lista->prox;
    lista->prox = elem;
    if (elem->prox)
        elem->prox->ant = elem;
    else
        lista->ultimo = elem;
}
```

---

### 3.2 Inserir depois de outro nó
```cpp
void inserir_depois(cabeca *lista, no *ref, no *elem) {
    elem->ant = ref;
    elem->prox = ref->prox;
    ref->prox = elem;
    if (elem->prox != NULL)
        elem->prox->ant = elem;
    else
        lista->ultimo = elem;
    lista->tam++;
}
```

---

### 3.3 Remover um nó
```cpp
void remover_no(cabeca *lista, no *lixo) {
    if (lista->prox == lixo)
        lista->prox = lixo->prox;
    else
        lixo->ant->prox = lixo->prox;
    
    if (lista->ultimo == lixo)
        lista->ultimo = lixo->ant;
    else
        lixo->prox->ant = lixo->ant;
    
    lista->tam--;
}
```

---

## 4) Lista Duplamente Encadeada Circular
- Não tem um final, permitindo percorrer em ambas as direções.

## 5) Lista Duplamente Encadeada Multilista
- Possui apontamentos independentes para o próximo e anterior, sem obrigatoriedade de apontamento recíproco.

---

Esse documento apresenta uma visão estruturada sobre listas encadeadas e suas operações fundamentais.

