# Guia de Ponteiros em C

## 1) Geral

- `int` = 4 bytes *(armazena o valor em binário)*
- `char` = 1 byte
- `%p` = mostra o endereço de um ponteiro
- `&variavel` = mostra o endereço da variável
- `*ponteiro` = ponteiro que aponta para o endereço de alguma variável

```c
int main() {
    int age = 1;
    int lane = 1;
    int *pAge = &age; // um ponteiro pAge que recebe o endereço de age

    printf("valor de age: %d \n", age);  // imprime o valor de age (1)
    printf("endereco de age: %p \n", &age);  // imprime o endereço de age

    printf("valor de pAge %d \n", *pAge);  // imprime o valor de age através do ponteiro
    printf("endereco de pAge %p \n", &pAge);  // imprime o endereço do ponteiro pAge
}
```

---

## 2) Passagem como Parâmetro em Funções

```c
void troca(int *p, int *q) { // ponteiros recebem endereços
    *p = 89;
    *q = 45;
}

int main() {
    int a = 3, b = 9;
    troca(&a, &b); // passando os endereços
    printf("%d %d\n", a, b); // imprime 89 e 45
}
```

---

## 3) Ponteiros x Arrays x Matrizes

- Em C, o nome do vetor `v` é equivalente ao endereço do seu primeiro elemento, ou seja, `&v[0]`.

```c
int main() {
    int v[2] = {1, 2}; // array
    int *p; // ponteiro de inteiro
    p = v; // ou p = &v[0]

    p[0] = 5; // alterando o primeiro valor do array

    printf("%d %d\n", p[0], p[1]); // imprime 5 e 2
    printf("%d %d\n", v[0], v[1]); // também imprime 5 e 2

    ///////////////////////////////////////////////////////////////////////////
    
    int m[2][2] = {{1, 2}, {3, 4}}; // matriz 2x2
    printf("%d\n", m[1][1]); // imprime o elemento da linha 2 e coluna 2

    p = m[0]; // ou (int *)m

    for (int i = 0; i < 4; i++)
        printf("%2d", p[i]); // imprime 1 2 3 4

    return 0;
}
```

---

## 4) Ponteiros x Structs

```c
typedef struct {
    int value;
} Point;

int main() {
    Point s;
    Point *ptr = &s;

    s.value = 20; // acesso via struct
    (*ptr).value = 40; // acesso via ponteiro (notação ponto)
    ptr->value = 30; // acesso via ponteiro (notação seta)

    printf("%d\n", s.value); // imprime 30
    return 0;
}
```


