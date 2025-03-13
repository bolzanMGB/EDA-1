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

- **Inordem:** primeiro a sub esquerda, depois a raiz, ultimo a sub direita. Nessa ordem: 3, 5, 4, 8, 2, 1, 9, 7, 6](
    Nessa ordem: 3, 5, 4, 8, 2, 1, 9, 7, 6
    
- **Pós-ordem:** primeiro a sub esquerda, depois a sub direita, por ultimo a raiz. Nessa ordem: 3, 4, 8, 5, 9, 1, 6, 7, 2;

### 4.6.2 Em largura:

- Utitliza uma fila;
- Enfileira os filhos;
-Nessa ordem: 2 5 7 3 8 1 6 4 9;
