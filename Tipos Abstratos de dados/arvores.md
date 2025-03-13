# Árvores

## 4.1 Genealogia:

![image](https://github.com/user-attachments/assets/976bff84-53c8-4283-ab19-3a3b58e296b2)

- **Pai e filho:** B é pai de E e F;
- **Irmãos:** B, C e D são irmãos;
- **Ancestrais:** G, D, A são os ancestrais de L;
- **Nível:** A tem nivel 0. B, C, D tem nível 1. E, F, G, H tem nível 2;
- **Altura:** a árvore do exemplo tem altura 4;
- **Folha/Terminal/Nó externo:** I, J, K, L, H, C são folhas (sem filhos);
- **Grau de um nó:** B tem grau 2 (dois filhos);
- **Grau de um árvore:** a árvore do exemplo tem grau 3 (máximo de filhos é 3);

## 4.2 Árvore Binária:

![image](https://github.com/user-attachments/assets/d1b9770b-120c-4c5e-9f50-bff96a3395fe)


## **4.3 Características:**

- Máximo de grau em um nó é dois;
- Formado por Raiz e Sub-Arvores Binárias;
- Ordem dos filhos é importante;

## **4. 4Classificação:**

- **Árvore Estritamente Binária:** nós tem 0 ou 2 filhos;
- **Árvore Binária Quase Completa:** todas as folhas estão no nivel d ou d-1;
- **Árvore Binária Completa:** todas as folhas estão em um mesmo nível;
- **Árvore Binária Cheia:** é uma árvore estritamente binária e completa;

## **4.5 Propriedades:**

- **Se há N nós internos, então a árvore tem:**
    - N + 1 nós externos;
- **Se a altura é h, então a árvore tem:**
    - No mínimo h nós internos;
    - No máximo 2^h - 1 nós internos;

## **4.6 Maneiras de Percorrer**
![image](https://github.com/user-attachments/assets/469ed62c-eeb6-4c34-8afb-79595c1681b5)
### **4.6.1 Em ordens: **

- **Pré-ordem:** primeiro a raiz, depois a sub esquerda, depois a sub direita. Nessa ordem: 2, 5, 3, 8, 4, 7, 1, 9, 6;

- **Inordem:** primeiro a sub esquerda, depois a raiz, ultimo a sub direita. Nessa ordem: 3, 5, 4, 8, 2, 1, 9, 7, 6];
    
- **Pós-ordem:** primeiro a sub esquerda, depois a sub direita, por ultimo a raiz. Nessa ordem: 3, 4, 8, 5, 9, 1, 6, 7, 2;

### 4.6.2 Em largura:

- Utitliza uma fila;
- Enfileira os filhos;
- Nessa ordem: 2 5 7 3 8 1 6 4 9;

## 4.7 Árvore binária de busca (ABB)

### 4.7.1 Estrutura:

- Combina a exibilidade da inserção nas lista encadeadas com a efciência da
busca nos vetores ordenados;
- Permite a busca binária de um nó a partir da raiz;
- Chaves: conteúdo dos nós;
- Todo nó não-terminal tem no máximo 2 filhos;
- Nó folha apontam para NULL (nós externos);
- Cada nó tem a chave maior que as chaves da sua subárvore esquerda;
- Cada nó tem a chave menor que as chaves da sua subárvore direita;

### 4.7.1 Buscar um valor:

- Ou o valor a ser buscado está na raiz da árvore:
- Ou é menor do que o valor da raiz:
    - Se estiver na árvore, está na subárvore esquerda;
- Ou é maior do que o valor da raiz:
    - Se estiver na árvore, está na subárvore direita;
    
 ![image](https://github.com/user-attachments/assets/a6c2d477-9f80-4a33-ae91-4d2f5890f5eb)
- Nessa ordem: 4, 1, 9, 2, 11, 6, 3, 7, 12, 8, 5, 10;
    

```cpp
#define info(A) (A.info)
#define key(A) (A.chave)
#define less(A, B) ((A) < (B))
#define eq(A, B) ((A) == (B))
#define exch(A, B) { Item t = A; A = B; B = t; }
#define compexch(A, B) if(less(B, A)) exch(A, B)

typedef int Key;
typedef struct data Item;
struct data {
    Key chave;
    char info[100];
};

typedef struct node STnode;
struct node {
    Item item;
    STnode *esq, *dir;
};

STnode *new(Item x, STnode *e, STnode *d) {
    STnode *no = malloc(sizeof(STnode));
    no->esq = e;
    no->dir = d;
    no->item = x;
    return no;
}

STnode *STsearch(STnode *no, Key v) {
    // condição de parada
    if (no == NULL || eq(v, key(no->item)))
        return no;

    // varrer subárvore esquerda; condição?
    if (less(v, key(no->item))) // como?
        return STsearch(no->esq, v);
    else
        return STsearch(no->dir, v);
}
```

### 4.72 Inserir um valor

```cpp
STnode *STinsert(STnode *no, Item item) {
    // condição de parada
    if (no == NULL) // alcançou um nó externo
        return new(item, NULL, NULL);

    Key novo = key(item);  // chave a ser inserida
    Key atual = key(no->item);  // chave nó verificado

    // decidir inserir na subárvore esquerda; condição?
    if (less(novo, atual)) // como?
        no->esq = STinsert(no->esq, item);
    else
        no->dir = STinsert(no->dir, item);

    return no;
}

int main(int argc, char *argv[]) {
    STnode *tree;
    for (int i = 0; i < n; i++) {
        Item v;
        scanf("%d %s", &v.chave, v.info);
        tree = STinsert(tree, v);
    }
}
```

### 4.7.4 Remover um nó:

```cpp
STnode *STdelete(STnode *no, Key remove) {
    // não achou
    if (no == NULL) return NULL;

    Key atual = key(no->item);

    // procure à esquerda
    if (less(remove, atual))
        no->esq = STdelete(no->esq, remove);

    // procure à direita
    else if (less(atual, remove))
        no->dir = STdelete(no->dir, remove);

    // eq(atual, remove) && somente 1 filho (??)

    // ou retorne o filho da esquerda ao seu avô
    else if (no->dir == NULL) {
        STnode *filho = no->esq;
        free(no);
        return filho;
    }

    // ou retorne o filho da direita ao seu avô
    else if (no->esq == NULL) {
        STnode *filho = no->dir;
        free(no);
        return filho;
    }

    // Se tiver os dois filhos
    else {
        remover_sucessor(no);
    }

    return no;
}

void remover_sucessor(STnode *raiz) {
    STnode *sucessor = raiz->dir;
    STnode *pai = raiz;

    // procurando o pai do sucessor
    // sucessor = menor dos maiores
    while (sucessor->esq != NULL) {
        pai = sucessor;
        sucessor = sucessor->esq;
    }

    // avô assume os filhos
    if (pai->esq == sucessor)
        pai->esq = sucessor->dir;
    else
        pai->dir = sucessor->dir;

    raiz->item = sucessor->item;
    free(sucessor);
}

// tree = STdelete(tree, c);
```

### 4.7.4 Outros:

```cpp
// achar o valor mínimo
STnode *minimo(STnode *no) {
    if (no->esq == NULL) return no;
    return minimo(no->esq);
}

// sucessor
STnode *sucessor(STnode *no) {
    if (no->dir != NULL) return minimo(no->dir);
    return ancestral_a_direita(no);
}

STnode *ancestral_a_direita(STnode *no) {
    if (no == NULL) return NULL;

    //não tenho pai = não ter ancestral OU
    // ser descendente esquerdo = primeiro ancestral é meu pai
    if (no->pai == NULL || no->pai->esq == no) // nó com campo pai
        return no->pai;

    // ser descendente direito > pai = procurar ancestral maior
    return ancestral_a_direita(no->pai);
}
```

### 4.7.5 Custos

- Não balaneadas:
    - Melhor caso: log N;
    - Caso médio:  log N ;
    - Pior caso: N;
- Balanceadas: log N (todos os casos);
