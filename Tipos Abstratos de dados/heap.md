# Fila de Prioridades

## Conceito

- É um tipo abstrato de dados (TAD);
- Acessado por uma interface (conjunto de operações);
- Não precisam estar totalmente ordenados;
- Nem todos os dados precisam sem processados.
- Dados rankeados por uma prioridade;
- O mais importante e saber quem está no topo;
- Mineração de dados, caminhos e3m grafos;
- Prioridade maxima ou prioridade minima (maior valor maior prioridade ou menor valor maior prioridade;

## Heap

### 1. Características:
![image](https://github.com/user-attachments/assets/55c893ce-179f-4317-b841-f8d050b2f9a7)

- Árvore binária quase completa:
    - Todas as folha no nível d ou d-1;
    - Todos os níveis exceto o último estão cheios;
    - Os nós do último nível estão mais a esquerda possível;
- A raiz é a chave de maior prioridade;
- Quanto mais próximo à raiz, maior a prioridade;
- Cada nó possui filhos com valores menores ou iguais;
- Acesso direto aos nós;
- **Heap Mínimo**: O valor do nó pai é **menor** que o dos filhos.
- **Heap Máximo**: O valor do nó pai é **maior** que o dos filhos.
- Representada por um vetor:
    - Raiz: posição 1 (k/2);
    - Filhos: posição 2 e 3 (2k e 2k+1);
    - Netos: posição 4,5,6,7;
    - ***Se o pai na pq[0]:
        - pai: k-1/2;
        - filhos: 2k+1 e 2k+2;
- **Se há N nós internos, então a árvore tem:**
    - **N + 1 nós externos;**
    - No mínimo lg (n+1) de altura;
    - No máximo N de altura;
- **Se a altura é h, então a árvore tem:**
    - No mínimo h nós internos;
    - No máximo 2^h - 1 nós internos;
![image](https://github.com/user-attachments/assets/42c0d182-1fc5-4340-bd85-3b914e591246)


### 2. Inserção:

- Subir de filho para pai fazendo swap até achar um menor ou chegar na raiz;
- Inserir no fim da lista: Filho é maior que o pai?
    - Sim: troca de lugar com o pai e compara com o pai do pai dele;
    - Não: está certo;
- // Complexidade: 1 + log N comparações O(log N)

```cpp
#define less(A, B) ((A) < (B))
#define exch(A, B) { Item t = A; A = B; B = t; }

// static: acessível somente no arquivo
static Item *pq;
static int N;

//  criar uma fila de prioridades com capacidade máxima inicial
void PQinit(int maxN) {
    pq = malloc(sizeof(Item) * (maxN + 1));
    N = 0;
}

// ve se esta vazia
int PQempty() {
    return N == 0;
}

// inserir uma chave
void PQinsert(Item v) {
    // adicionar no fim
    pq[++N] = v;

    // consertar o elemento na posição N
    fixUp(N);
}

void fixUp(int k) {
    // k até 1 - reduzindo metade por iteração
    // altura da árvore ≈ log k
    while (k > 1 && less(pq[k / 2], pq[k])) {
        exch(pq[k], pq[k / 2]);
        k = k / 2;
    }
}
```

### 3. Remoção

- Trocar o topo pelo ultimo, se o N for menor que os filhos, fazer swap com o maior;
- Isso até N ser maior ou igual aos filhos ou ser uma folha;
- troca topo pelo ultimo:
    - achar filho maior:
    - ultimo é menor que seu maior filhos?
        - sim: troca com o filho da direita;
        - nao: ta no lugar certo;
- Complexidade: 2 log N comparações - O(log N)

```cpp
// retornar e remover (maior prioridade)
Item PQdelmax() {
    // troque topo -> último
    exch(pq[1], pq[N]);

    // reposicione
    fixDown(1, N - 1);

    // retorne o removido
    return pq[N--];
}

void fixDown(int k, int N) { // afunda k
    // enquanto tiver filho
    while (2 * k <= N) {
        int j = 2 * k; // filho da esquerda

        // se tiver filho da direita e for maior
        if (j < N && less(pq[j], pq[j + 1])) j++;

        // pq[k] maior que o maior filho?
        if (!less(pq[k], pq[j])) break;

        // senão, afunde (troque com o filho)
        exch(pq[k], pq[j]);

        // atualiza k para o maior filho
        k = j;
    }
}

```

### 4 Alterar Prioridade

- Significa modificar o valor da chave associada a um determinado item e, em seguida, reorganizar a estrutura da heap para manter as propriedades do heap binário.

```cpp
typedef struct {
    char nome[20];
    int chave;
} Item;

static int *pq;
static int *qp;
static int N;

void PQinit(int);
void PQinsert(int);
void PQchange(int);
int PQdelmax();

void PQchange (int i) {
// atualizar data [i] na fila
// data [i] est á na posi ção qp[i]
fixUp ( qp [i ]) ;
fixDown ( qp [i] , N) ;
}

int main() {
    Item data[6] = {
        {"José", 10},
        {"Maria", 9},
        {"Júlio", 4},
        {"Paulo", 23},
        {"Ana", 30},
        {"Carla", 17}
    };

    PQinit(6);
    for (int i = 0; i < 6; i++) PQinsert(i);

    data[0].chave = 50;
    PQchange(0);

    int k = PQdelmax();
    printf("%d %s\n", data[k].chave, data[k].nome);
    
    return 0;
}
```

