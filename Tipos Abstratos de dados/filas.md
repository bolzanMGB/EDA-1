# 1. Filas

## 1.1. Definição e características:

- Segue o princípio FIFO (First In, First Out);
- Alinhamento de uma série de indivíduos ou objetos em sequência, de modo que um esteja imediatamente atrás do outro;
- Ordem de chegada: os que estão na frente são processados primeiro;
- Inserções no fim, remoções no início;
- Tempo de execução: Operações básicas são O(1) (tempo constante);

![image.png](attachment:f7a8012b-03c6-4f6d-8c40-3877598fa183:image.png)

## 1.2. Fila estática circular:

- Usa um array fixo, porém ao invés de deixar espaço vazio ao remover elementos ela reutiliza os índices do array;
- Evita desperdício de memória;
- O índice de inserção (`u`) e o índice de remoção (`p`) voltam ao início do array quando atingem o fim

```cpp
#define N 7
int fila[N];
int p, u;

void criar_fila()
{
    p = u = 0;
}

int vazia ()
{
	return p == u;
}

// Adição no fim da fila
void enfileira(int y) {
    fila[u++] = y;
    if (u == N) u = 0;  // Caso o índice atinja o final, volta ao início (fila circular)
}

// Remoção no início da fila 
int desenfileira() {
    int x = fila[p++];
    if (p == N) p = 0;  // Caso o índice atinja o final, volta ao início (fila circular)
    return x;
}

enfileira(10), enfileira(20), enfileira(30), enfileira(40)
Fila: [10] [20] [30] [40] [ ] [ ] [ ]
         ↑p               ↑u
enfileira(50), enfileira(60)
Fila: [10] [20] [30] [40] [50] [60] [ ]
         ↑p                         ↑u
desenfileira(), desenfileira() 
Fila: [10] [20] [30] [40] [50] [60] [ ]
                 ↑p                 ↑u
enfileira(70), enfileira(80)
Fila: [70] [80] [30] [40] [50] [60] [ ]
            ↑u  ↑p

```

## 1.3. Fila estáticaDinâmica:

```cpp
typedef int Item;

typedef struct {
    Item *item; // ponteiro para o bloco de memoria que irá conter os itens
    int primeiro, ultimo;
} Fila;

Fila *criar(int maxN) {
    Fila *p = malloc(sizeof(Fila));
    p->item = malloc(maxN * sizeof(Item));
    p->primeiro = p->ultimo = 0;
    return p;
}

int vazia(Fila *f) { // retorna se fila esta vazia
    return f->primeiro == f->ultimo;
}

	void enfileira(Fila *f, int y) { // em c ponteiros podem ser usados como arrays
    f->item[f->ultimo++] = y; // f->item[i] mesma coisa que *(f->item + i)
}

int desenfileira(Fila *f) {
    return f->item[f->primeiro++]; // vai andar com a fila
}

void imprime(Fila *f) {
    printf("\nFILA p=%d e u=%d\n", f->primeiro, f->ultimo);
    for (int i = f->primeiro; i < f->ultimo; i++) {
        printf(" F[%d] |", i);
    }
    printf("\n");

    for (int i = f->primeiro; i < f->ultimo; i++) {
        printf(" %3d |", f->item[i]);
    }
    printf("\n");
}

int main() {
    printf("\n\nCriando a fila e enfileirando 10 elementos \n");
    Fila *fila1 = criar(100);
    for (int i = 0; i < 10; i++) {
        enfileira(fila1, i);
    }
    imprime(fila1);

    printf("\n\nDesenfileirando os 3 primeiros elementos \n");
    for (int i = fila1->primeiro; i < 3; i++) {
        desenfileira(fila1);
    }
    imprime(fila1);

    Fila *fila2 = criar(400);
    // Continuação do código
    return 0;
}
```

## 1.4. Implementação com lista encadeada

```cpp
void enfileira(cabeca *lista, no *novo) {
    no *novo = criar_no(x); // Criação de novo nó
    if (novo) {
        if (vazia(lista))
            lista->prox = novo; // Caso fila esteja vazia
        else
            lista->ultimo->prox = novo; // Atualiza o último elemento
        
        lista->ultimo = novo; // Novo elemento se torna o último
        novo->prox = NULL;    // Aponta para NULL
        lista->tam++;         // Incrementa o tamanho da fila
    }
}

Antes de enfileirar:
Cabeça -> Elemento 1 -> Elemento 2 -> NULL
Cauda -----------------------------^

Após enfileirar:
Cabeça -> Elemento 1 -> Elemento 2 -> Elemento 3 -> NULL
Cauda --------------------------------------------^

```

```cpp
Item desenfileira(cabeca *lista) {
    no *lixo = lista->prox; // Ponteiro para o elemento a ser removido
    lista->prox = lixo->prox; // Avança a cabeça da fila

    if (vazia(lista))
        lista->ultimo = NULL; // Atualiza último se fila estiver vazia
    
    lista->tam--;             // Decrementa tamanho da fila
    Item x = lixo->info;      // Captura o valor do elemento removido
    free(lixo);               // Libera memória do nó removido
    return x;                 // Retorna valor do elemento removido
}

Antes de desenfileirar:
Cabeça -> Elemento 1 -> Elemento 2 -> NULL
Cauda -----------------------------^

Após desenfileirar:
Cabeça -> Elemento 2 -> NULL
Cauda ------------------^

```
