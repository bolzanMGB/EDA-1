# 📌 Alocacao de Memoria em C

## 1️⃣ Tipos de Espaço de Endereços

### 1.1 Text;
- Contém o código do programa e constantes;

### 1.2 Data;
- Armazena variáveis globais e estáticas;

### 1.3 Stack;
- Contém a pilha de execução, armazenando parâmetros e variáveis locais;

### 1.4 Heap;
- Contém blocos de memória alocados dinamicamente durante a execução;

---

## 2️⃣ Tipos de Alocação de Memória

### 2.1 Alocação Estática;
- Ocorre quando são declaradas variáveis globais ou estáticas;
- Geralmente alocadas na *Data*;
- Mantêm seu valor durante toda a vida do programa;

```c
#include <stdio.h>

int a = 0;  // Variável global (alocação estática)

void incrementa(void) {
    int b = 0; // Variável local (alocação automática)
    static int c = 0; // Variável local estática

    printf("a: %d, b: %d, c: %d\n", a, b, c);
    a++;
    b++;
    c++;
}

int main(void) {
    for (int i = 0; i < 5; i++)
        incrementa();
    return 0;
}
```

---

### 2.2 Alocação Automática;
- Ocorre com variáveis locais e parâmetros de função;
- Utiliza a pilha (*stack*), sendo automaticamente desalocada ao fim da função;

---

### 2.3 Alocação Dinâmica;
- O programa solicita memória ao sistema durante a execução;
- Geralmente alocada na *heap*;
- O programador é responsável por liberar a memória alocada;

---

## 3️⃣ Operadores de Alocação de Memória

### 3.1 `sizeof`;
Retorna o tamanho de um dado em bytes;

```c
#include <stdio.h>

struct endereco {
    char rua[100];
    int numero;
};

int main() {
    printf("%lu bytes \n", sizeof(int)); // 4 bytes
    printf("%lu bytes \n", sizeof(struct endereco)); // 104 bytes
    return 0;
}
```

### 3.2 `malloc`;
Aloca um bloco de memória do tamanho desejado;

```c
int *p = (int *) malloc(sizeof(int));
```

### 3.3 `calloc`;
Aloca um array de `A` elementos de tamanho `N` bytes e inicializa com 0;

```c
int *p = (int *) calloc(5, sizeof(int));
```

### 3.4 `realloc`;
Redimensiona um bloco de memória previamente alocado;

```c
int *p = malloc(sizeof(int));
p = realloc(p, 4 * sizeof(int));
free(p);
```

### 3.5 `free`;
Libera o espaço apontado por um ponteiro;

```c
free(p);
```

