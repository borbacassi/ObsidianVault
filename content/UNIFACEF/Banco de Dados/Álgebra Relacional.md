## Categorias de Linguagem:

`Formais:`
- Álgebra
- Cálculo Relacional
`Comerciais:`
- SQL

## Características

- Orientadas a conjuntos;
- Linguagem de base:
  -  Linguagens relacionais devem ter no mínimo um poder de expressão equivalente ao de uma linguagem formal
- Fechamento:
  - Resultados das consultas são relações
- **Operadores** para consulta e alteração das relações (Conjuntos)
- Linguagem procedural
   - Uma expressão na álgebra define uma execução sequencial de operadores
   - A execução de cada operador produz uma relação

## Classificação dos operadores

`Fundamentais:`
 - Unário: Seleção e Projeção
 - Binários: Produto cartesiano, união e diferença

`Derivados:`
- Binários : intersecção, junção e divisão

`Especiais:`
- Renomeação (união) e atribuição
- Operador de alteração (unário)

# Detalhes das operações

`Básicas:`
- Oriundas da teoria dos conjuntos: produto cartesiano, união e diferença;
- Específicas para relações: seleção, projeção e renomeação.

`Adicionais:`
- Provenientes da teoria de conjuntos: intersecção
- Específicas para relações: divisão e junção;

Obs: 
• As operações básicas são suficientes para exprimir as mesmas consultas que o cálculo relacional
• As operações adicionais auxiliam a formular certas consultas que seriam complexas de exprimir usando apenas as operações básicas.


## Operações

 `União`:  r U s
 - Retorna a união das tuplas de duas relações R1 e R2
 - Eliminação automática de duplicatas
 - Notação:  relação1 U relação2


![[Pasted image 20260410200926.png]]

 
`Diferença:`  r - s

- Retorna as tuplas presentes em R1 e ausentes em R2 
- Notação: • relação1 - relação2

![[Pasted image 20260410201042.png]]

`Produto Cartesiano:` r x s

- Retorna todas as combinações de tuplas de duas relações R1 e R2 
- Grau do Resultado • Grau (R1 ) + Grau (R2 ) 
- Cardinalidade do Resultado:
   • Cardinalidade (R1 ) * Cardinalidade (R2 ) 
- Notação: • relação1 X relação2;

![[Pasted image 20260410203722.png]]


`Intersecção:`  r ∩ s

- Retorna as tuplas comuns em R1 e R2;
- Notação:   relação1 ∩ relação;

![[Pasted image 20260410203042.png|697]]

`Divisão`:






 
 

[^1]: Unario = precisa de um, binario = 2 
