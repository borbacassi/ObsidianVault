# Pilha
> Estrutura de dados que usa um vetor como base, permitindo inserções no final da fila.
> 	`LIFO - Last in, First Out
> Pilhas são usadas em tarefas computacionais que requerem a inversão da ordem da entrada de dados.
### Construção
```javascript
export default class Stack {

    #data       // Vetor privado

    constructor() {
        this.#data = []     // Vetor vazio
    }
```

# Fila

> Lista linear de acesso restrito, que permite apenas as operações de enfileiramento (enqueue) e desenfileiramento (dequeue), a primeira ocorrendo no final da estrutura e a segunda no inicio da estrutura.
> `FIFO - First in, First Out`
> Principal aplicação: processamento de tarefas por ordem de chegada.

<colocar construção aqui>

# Deque

> Double-ended Queue
> Permite as mesmas operações de fila nas duas extremidades da estrutura
> `NÂO É FIFO`
> Principal aplicação: situações que precisam aceitar a inserção de itens prioritários e a desistência do último item.

# Lista Encadeada
> Estrutura de dados formada por unidades de informação chamadas **nodos** ou **nós**

### Nodos
Cada nodo possui duas partes: uma que armazena a informação e outra que guarda o endereço do próximo nodo da sequência.
A qualquer momento, temos um conhecimento apenas limitado de onde se encontram todos os nodos da lista. Sabemos apenas onde está o primeiro e o último nodo da sequência. Os nodos intermediários precisam ser encontrados partindo-se do primeiro e percorrendo a sequência.

### Construção
```javascript
export default class LinkedList {/* Classe que representa a estrutura de dados lista encadeada */

    #head       // Início da lista (cabeça)
    #tail       // Fim da lista (cauda)
    #count      // Quantidade de nodos da lista

    constructor() {
        this.#head = null
        this.#tail = null
        this.#count = 0        
    }
    /* Classe que representa a unidade de armazenamento da lista encadeada */
class Node {
    constructor(val) {
        this.data = val     // Informação relevante para o usuário
        this.next = null    // Ponteiro para o próximo nodo da sequência
    }
}

```

# [[Lista Duplamente Encadeada]]
>Estrutura também formada por nodos.
>Cada nodo possui 3 partes:
>`data` -> armazena informação.
>`prev` -> guarda o endereço do nodo anterior.
>`next` -> guarda o endereço do nodo seguinte.
>A qualquer momento, temos um conhecimento apenas limitado de onde se encontram todos os nodos da lista. Sabemos apenas onde está o primeiro e o último nodo da sequência. Os nodos intermediários precisam ser encontrados partindo-se do primeiro  **OU** do último nodo e percorrendo a sequência.

### Construção
```javascript
class Node {
  constructor(val) {
    this.prev = null;
    this.data = val;
    this.next = null;
  }
}

export default class DoublyLinkedList {
  #head;
  #tail;
  #count;

  constructor() {
    this.#head = null;
    this.#tail = null;
    this.#count = 0;
  }

```

