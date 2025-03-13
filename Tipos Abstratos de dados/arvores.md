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

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/787a1cee-61ed-4b32-8440-b0cf3286709d/b9576a2b-e96d-4f0d-94ac-c60b0be09bd8/image.png)

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

## **4.6 Implementação**

![image.png](attachment:5c22f67e-e497-4e6b-80f2-92fbea93f15e:image.png)

```cpp
typedef int Item;

typedef struct node no;
struct node
{
    Item item;
    no *pai;
    no *esq, *dir;
};

no *criar_arvore(Item x, no *p, no *e, no *d)
{
    no *raiz = malloc(sizeof(no));
    raiz->pai = p;
    raiz->esq = e;
    raiz->dir = d;
    raiz->item = x;
    return raiz;
}

no *avo(no *elemento) {
    if ((elemento != NULL) && (elemento->pai != NULL))
        return elemento->pai->pai;
    return NULL;
}

no *tio(no *elemento) {
    no *vo = avo(elemento);
    if (vo == NULL) return NULL;

    if (elemento->pai == vo->esquerda)
        return vo->direita;
    return vo->esquerda;
}

no *irmao(no *elemento) {
    if ((elemento != NULL) && (elemento->pai != NULL)) {
        if (elemento == elemento->pai->esquerda)
            return elemento->pai->direita;

        return elemento->pai->esquerda;
    }
}

no *busca_linear(no *raiz, Item v) {
    if (raiz == NULL) return NULL;  // Se a árvore for vazia, retorna NULL
    if (raiz->item == v) return raiz;  // Se encontrou o valor, retorna o nó

    // Busca na subárvore esquerda
    no *encontrado = busca_linear(raiz->esq, v);
    if (encontrado) return encontrado;  // Se achou, retorna o nó

    // Busca na subárvore direita
    return busca_linear(raiz->dir, v);
}

int numero_nos(no *raiz) {
    if (raiz == NULL) return 0;
    return 1 + numero_nos(raiz->esq) + numero_nos(raiz->dir);
}

int altura(no *raiz) {
    if (raiz == NULL) return 0;
    return 1 + fmax(altura(raiz->esq), altura(raiz->dir));
}

```

### **4.6.1 Em ordens: RED**

- **Pré-ordem:** primeiro a raiz, depois a sub esquerda, depois a sub direita;
    
    ![Nessa ordem: 2, 5, 3, 8, 4, 7, 1, 9, 6](https://prod-files-secure.s3.us-west-2.amazonaws.com/787a1cee-61ed-4b32-8440-b0cf3286709d/3c79c077-0c71-40ee-8b79-5af57424f52f/image.png)
    
    Nessa ordem: 2, 5, 3, 8, 4, 7, 1, 9, 6
    

- **Inordem:** primeiro a sub esquerda, depois a raiz, ultimo a sub direita;
    
    ![Nessa ordem: 3, 5, 4, 8, 2, 1, 9, 7, 6](https://prod-files-secure.s3.us-west-2.amazonaws.com/787a1cee-61ed-4b32-8440-b0cf3286709d/2fc1937f-c345-416e-afb6-d5570b7657c4/image.png)
    
    Nessa ordem: 3, 5, 4, 8, 2, 1, 9, 7, 6
    

- **Pós-ordem:** primeiro a sub esquerda, depois a sub direita, por ultimo a raiz.
    
    ![Nessa ordem: 3, 4, 8, 5, 9, 1, 6, 7, 2](https://prod-files-secure.s3.us-west-2.amazonaws.com/787a1cee-61ed-4b32-8440-b0cf3286709d/59d2054d-a09d-4ec8-9392-ae0e24b2585b/image.png)
    
    Nessa ordem: 3, 4, 8, 5, 9, 1, 6, 7, 2
    
- Implementação com recursão
    
    ```cpp
    
    // com recursão
    void preordem(no *raiz) {
        if (raiz != NULL) {
            printf("%d ", raiz->dado); /* visita / processa raiz */
            preordem(raiz->esq);
            preordem(raiz->dir);
        }
    }
    
    void inordem(no *raiz) {
        if (raiz != NULL) {
            inordem(raiz->esq);
            printf("%d ", raiz->dado); /* visita / processa raiz */
            inordem(raiz->dir);
        }
    }
    
    void posordem(no *raiz) {
        if (raiz != NULL) {
            posordem(raiz->esq);
            posordem(raiz->dir);
            printf("%d ", raiz->dado); /* visita / processa raiz */
        }
    }
    
    ```
    
- Implementação sem recursão
    
    ```cpp
    // sem recursao
    void pre_ordem(no *raiz) {
        cabeca *p;
        p = criar_lista();
    
        empilha(p, raiz);
    
        while (!vazia(p)) {
            raiz = desempilha(p);
    
            if (raiz != NULL) {
                // processa a raiz
                printf("%d ", raiz->dado);
    
                // empilhar nó direita ou esquerda?
                empilha(p, raiz->dir);
                empilha(p, raiz->esq);
            }
        }
        free(p);
    }
    
    void in_ordem(no *raiz) {
        cabeca *p = criar_lista();
        // empilha todos os nós à esquerda
        while (raiz != NULL) {
            empilha(p, raiz);
            raiz = raiz->esq;
        }
    
        // visita os nós empilhados
        // qual o primeiro nó a ser visitado?
        while (!vazia(p)) {
            raiz = desempilha(p);
            if (raiz != NULL) {
                // processa o nó mais à esquerda
                printf("%d ", raiz->dado);
    
                // nós à direita do mais à esquerda
                raiz = raiz->dir;
                while (raiz != NULL) {
                    empilha(p, raiz);
                    raiz = raiz->esq;
                }
    
                // qual o próximo nó a ser visitado?
            }
        }
        free(p);
    }
    
    void pos_ordem(no *raiz) {
        cabeca *p, *raizes;
        p = criar_lista();       // pilha para percurso
        raizes = criar_lista();  // pilha para raízes
    
        empilha(p, raiz);
        while (!vazia(p)) {
            raiz = desempilha(p);
            if (raiz != NULL) {
                // visita a raiz e processa depois
                empilha(raizes, raiz);
    
                // subárvore esquerda
                if (raiz->esq) empilha(p, raiz->esq);
                if (raiz->dir) empilha(p, raiz->dir);
    
                // visitar da dir. p/ esq. (??)
                // processar na ordem inversa
            }
        }
    
        // processar raízes
        while (!vazia(raizes)) {
            raiz = desempilha(raizes);
            printf("%d ", raiz->dado);
        }
    }
    
    ```
    

### 4.6.3 Em largura:

- Utitliza uma fila;
- Enfileira os filhos;

![Nessa ordem: 2 5 7 3 8 1 6 4 9](https://prod-files-secure.s3.us-west-2.amazonaws.com/787a1cee-61ed-4b32-8440-b0cf3286709d/a9714371-eb8a-472b-8f61-fc34c00702ca/image.png)

Nessa ordem: 2 5 7 3 8 1 6 4 9
