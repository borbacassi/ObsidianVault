
> **Estrutura de dados** onde cada elemento aponta tanto para o próximo quanto para o anterior, formando uma "corrente" bidirecional.
---

##  O que é?

Uma **Lista Duplamente Encadeada** é uma estrutura de dados linear composta por **nodos** (nodes) conectados entre si. Diferente de um array, os elementos não ficam em posições contíguas na memória — cada um "sabe" onde está o seu vizinho.

```
null ← [A] ⇄ [B] ⇄ [C] ⇄ [D] → null
        ↑                    ↑
       head                 tail
```

---

##  Bloco 1 — O Nodo (`Node`)

Cada elemento da lista é um **nodo**. Ele carrega três informações:

```javascript
class Node {
  constructor(val) {
    this.prev = null;  // aponta para o nodo ANTERIOR
    this.data = val;   // o VALOR armazenado
    this.next = null;  // aponta para o próximo nodo
  }
}
```

### Visualização de um nodo

```
┌──────┬──────┬──────┐
│ prev │ data │ next │
└──────┴──────┴──────┘
```

|Propriedade|Tipo|Descrição|
|---|---|---|
|`prev`|Node|Referência ao nodo anterior (`null` se for o primeiro)|
|`data`|qualquer|O valor/dado armazenado|
|`next`|Node|Referência ao próximo nodo (`null` se for o último)|

---

##  Bloco 2 — A Classe Principal (`DoublyLinkedList`)

```javascript
export default class DoublyLinkedList {
  #head;   // primeiro nodo da lista
  #tail;   // último nodo da lista
  #count;  // quantidade de nodos
```

> ⚠️ O `#` indica campos **privados** (encapsulamento). Só são acessíveis dentro da própria classe.

### Propriedades internas

|Campo|Descrição|
|---|---|
|`#head`|Aponta para o **primeiro** nodo|
|`#tail`|Aponta para o **último** nodo|
|`#count`|Número total de elementos na lista|

---

##  Bloco 3 — Getters e método privado

### `isEmpty` e `count`

```javascript
get isEmpty() {
  return this.#count === 0;  // true se a lista não tiver nenhum elemento
}

get count() {
  return this.#count;  // retorna o total de elementos
}
```

### `#findNode(pos)` — Busca otimizada pelo índice

Encontra um nodo por posição. A otimização está em **decidir de qual lado começar a busca**:

```javascript
#findNode(pos) {
  if (pos < this.#count / 2) {
    // posição está na primeira metade → começa do HEAD
    node = this.#head;
    for (let i = 0; i < pos; i++) node = node.next;
  } else {
    // posição está na segunda metade → começa do TAIL
    node = this.#tail;
    for (let i = this.#count - 1; i > pos; i--) node = node.prev;
  }
}
```

```
Lista com 6 elementos, posições 0..5

  0   1   2  |  3   4   5
[A]–[B]–[C]  | [D]–[E]–[F]
  ↑ busca    |       busca ↑
 do HEAD     |      do TAIL
```

> 💡 Isso reduz o número de iterações para no máximo **n/2**, tornando a busca mais eficiente.

---

##  Bloco 4 — Inserção (`insert`)

A inserção cobre **4 casos**:

### Caso 1 — Lista vazia

```javascript
if (this.isEmpty) {
  this.#head = inserted;
  this.#tail = inserted;
}
```

```
[novo] ← head e tail apontam para o mesmo nodo
```

### Caso 2 — Inserir no início (`pos === 0`)

```javascript
inserted.next = this.#head;
this.#head.prev = inserted;
this.#head = inserted;
```

```
Antes:  [A] → [B] → [C]
Depois: [novo] → [A] → [B] → [C]
```

### Caso 3 — Inserir no fim (`pos >= count`)

```javascript
inserted.prev = this.#tail;
this.#tail.next = inserted;
this.#tail = inserted;
```

```
Antes:  [A] → [B] → [C]
Depois: [A] → [B] → [C] → [novo]
```

### Caso 4 — Inserir no meio

```javascript
let nodePos = this.#findNode(pos);  // nodo que está na posição alvo
let before = nodePos.prev;          // nodo anterior a ele

before.next = inserted;    // antes aponta para o novo
inserted.prev = before;    // novo aponta de volta para antes
inserted.next = nodePos;   // novo aponta para o atual da posição
nodePos.prev = inserted;   // atual passa a apontar para o novo
```

```
Antes:  [A] ⇄ [C]
Depois: [A] ⇄ [novo] ⇄ [C]
```

### Atalhos de inserção

```javascript
insertHead(val) { this.insert(0, val); }
insertTail(val) { this.insert(this.#count, val); }
```

---

##  Bloco 5 — Remoção (`remove`)

A remoção também cobre **4 casos**:

### Caso 1 — Lista vazia ou posição inválida

```javascript
if (this.isEmpty || pos < 0 || pos > this.#count - 1) return undefined;
```

### Caso 2 — Remover o primeiro nodo (`pos === 0`)

```javascript
removed = this.#head;
this.#head = removed.next;
if (this.#head) this.#head.prev = null;   // novo head não tem anterior
if (this.#count === 1) this.#tail = null; // lista ficará vazia
```

### Caso 3 — Remover o último nodo (`pos === count - 1`)

```javascript
removed = this.#tail;
this.#tail = removed.prev;
if (this.#tail) this.#tail.next = null;   // novo tail não tem próximo
if (this.#count === 1) this.#head = null; // lista ficará vazia
```

### Caso 4 — Remover do meio

```javascript
removed = this.#findNode(pos);
let before = removed.prev;
let after = removed.next;

before.next = after;   // pula o nodo removido
after.prev = before;   // fecha o "buraco" pelo lado anterior
```

```
Antes:  [A] ⇄ [B] ⇄ [C]
                ↑ remover B
Depois: [A] ⇄ [C]
```

### Atalhos de remoção

```javascript
removeHead() { return this.remove(0); }
removeTail() { return this.remove(this.#count - 1); }
```

> Ambos retornam o **valor** (`data`) do nodo removido.

---

## Bloco 6 — `peek(pos)` (método vazio)

```javascript
peek(pos) {
  // não implementado ainda
}
```

> O `peek` é o método para **consultar** o valor de uma posição sem remover o nodo. A implementação seria simples:
> 
> ```javascript
> peek(pos) {
>   if (this.isEmpty || pos < 0 || pos >= this.#count) return undefined;
>   return this.#findNode(pos).data;
> }
> ```

---

##  Resumo de Complexidade

|Operação|Complexidade|
|---|---|
|`insert` (início/fim)|O(1)|
|`insert` (meio)|O(n/2) = O(n)|
|`remove` (início/fim)|O(1)|
|`remove` (meio)|O(n/2) = O(n)|
|`#findNode`|O(n/2) = O(n)|
|`peek`|O(n/2) = O(n)|

---

##  Comparativo: Array vs Lista Encadeada

|Característica|Array|Lista Duplamente Encadeada|
|---|---|---|
|Acesso por índice|O(1) ✅|O(n) ❌|
|Inserção no início|O(n) ❌|O(1) ✅|
|Inserção no fim|O(1)* ✅|O(1) ✅|
|Inserção no meio|O(n) ❌|O(n) ❌|
|Remoção no início|O(n) ❌|O(1) ✅|
|Uso de memória|Contígua|Dispersa (ponteiros extras)|
|Percurso reverso|Simples|Simples (via `prev`)|

---

##  Fluxo completo de inserção

```
insert(pos, val)
      │
      ├─ isEmpty? ──→ head = tail = novo nodo
      │
      ├─ pos === 0? ──→ novo.next = head → head.prev = novo → head = novo
      │
      ├─ pos >= count? ──→ novo.prev = tail → tail.next = novo → tail = novo
      │
      └─ else ──→ #findNode(pos) → reconectar os ponteiros → inserir no meio
```

---
