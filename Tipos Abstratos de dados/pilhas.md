# 2. Pilhas

## 2.1. Definição e características:

- Segue o princípio LIFO (Last In, First Out);
- O elemento removido é o que está na estrutura há *menos* tempo;
- O primeiro objeto a ser inserido na pilha é o último a ser removido;
- Inserção e remoção oncorrem no topo da pilha;
- O índice `t` indica a primeira posição vaga do vetor e `t-1` é o índice do topo da pilha;
- A pilha está vazia se t vale `0` e cheia se `t` vale `N`;

![image](https://github.com/user-attachments/assets/596578df-4562-453b-ad34-76414340dc12)

## 2. Funcionalidades das pilhas:

- Desfazer/Refazer;
- Histórico de navegadores;
- Gerenciamento de memória: pilhas de memória são utilizadas para armazenar todas as variáveis de um programa em execução;
- Recursão: as chamadas de função são mantidas por pilha de memória;
- Busca em profundidade: percorrer uma possibilidade completa antes de analisar o próximo caminho;
- Backtracking: poder voltar a um ponto para refazer uma decisão;
- Inversão de strings;
- Balanceamento de símbolos ([{}]): vericação sintaxe (compiladores);
- Identicador de expressões/palavras (tokens): vericação léxica (compiladores);
- Conversão de expressões: infixo para prefixo, posfixo para infixo, etc.

## 2.3.  Pilhas com listas estáticas:

- Item é um array;
- Empilha: coloca  X no topo e aumenta o topo;
- Desempilha: decrementa o topo em um (não remove);

```cpp
typedef char Item;

typedef struct {
    Item *item;
    int topo;
} Pilha;

Pilha *criar(int maxN) {
    Pilha *p = malloc(sizeof(Pilha));
    p->item = malloc(maxN * sizeof(Item)); // Aloca memória para os itens
    p->topo = 0; // Inicializa o topo
    return p;
}

int vazia(Pilha *p) {
    return p->topo == 0; // Verifica se a pilha está vazia, se t é igual a N
}

void empilhar(Pilha *p, Item item) {
    p->item[p->topo++] = item; // Empilha o item em t e depois incrementa t
}

Item desempilhar(Pilha *p) {
    return p->item[--p->topo]; // Decrementa t, remove o item e retorna o item desempilhado
}

Item espiar(Pilha *p) {
    return p->item[p->topo - 1]; // Retorna o item no topo sem remove-lo
}

empilha (A), empilha (B), empilha (C)
[A] [B] [C] [ ] [ ]
						 T	
desempilha ()
[A] [B] [C] [ ] [ ]
				 T	
empilha (D)
[A] [B] [D] [ ] [ ]
				     T	
	
```

## 2.4. Implementação com lista encadeada:

- Nós são implementados no começo da  lista;
- ultimo é o primeiro no a ser inserido na pilha;
- prox é quem esta no topo da pilha;

```cpp
// head aponta para o nó inicial e possui um ponteiro para o próximo nó e o número total de itens.
// no contem info e prox.
void empilha(head *lista, Item x) {
    node *novo = criar_no(x); 
    if (novo) {
        if (vazia(lista))
            lista->ultimo = novo;

        novo->prox = lista->prox;
        lista->prox = novo; 

        lista->num_itens++;
    }
}

Item desempilha(head *lista) {
    node *topo = lista->prox;
    lista->prox = topo->prox; // ⇐=

    if (topo == lista->ultimo)
        lista->ultimo = NULL;

    lista->num_itens--;

    Item x = topo->info; // ⇐=
    free(topo);          // ⇐=
    return x;            // ⇐=
}

Item espia(head *p) {
    return (p->prox->info);
}

head->NULL
    
empilha (A)
head->[A]->NULL
       P=U
empilha (B), empilha(C)
head->[B]->[A]->NULL
       P         U
desempilha ()
head->[A]->NULL
       P=
       U
```
