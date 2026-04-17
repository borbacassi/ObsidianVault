# Diagrama de Classes — Sistema de Pedidos

```plantuml
@startuml

skinparam classAttributeIconSize 0
skinparam classFontStyle bold
skinparam backgroundColor #FAFAFA
skinparam class {
  BackgroundColor #EEF2FF
  BorderColor #4F46E5
  ArrowColor #4F46E5
}

' ─────────────────────────────
' INTERFACE
' ─────────────────────────────
interface Pagavel {
  + processar(): boolean
  + cancelar(): boolean
  + getStatus(): String
}

' ─────────────────────────────
' CLASSE ABSTRATA
' ─────────────────────────────
abstract class Pessoa {
  - id: int
  # nome: String
  # email: String
  + getNome(): String
  + {abstract} getDadosCompletos(): String
}

' ─────────────────────────────
' CLASSES CONCRETAS
' ─────────────────────────────
class Cliente {
  - cpf: String
  - endereco: String
  + getDadosCompletos(): String
  + fazerPedido(): Pedido
}

class Funcionario {
  - matricula: String
  - cargo: String
  + getDadosCompletos(): String
}

class Pedido {
  - id: int
  - data: Date
  - status: String
  + calcularTotal(): double
  + cancelar(): void
}

class ItemPedido {
  - quantidade: int
  - precoUnitario: double
  + calcularSubtotal(): double
}

class Produto {
  - id: int
  - nome: String
  - preco: double
  - estoque: int
  + verificarDisponibilidade(): boolean
}

' ─────────────────────────────
' IMPLEMENTAÇÕES DE Pagavel
' ─────────────────────────────
class PagamentoCartao {
  - numeroCartao: String
  - bandeira: String
  + processar(): boolean
  + cancelar(): boolean
  + getStatus(): String
}

class PagamentoPix {
  - chave: String
  - qrCode: String
  + processar(): boolean
  + cancelar(): boolean
  + getStatus(): String
}

class PagamentoBoleto {
  - codigoBarras: String
  - vencimento: Date
  + processar(): boolean
  + cancelar(): boolean
  + getStatus(): String
}

' ─────────────────────────────
' RELACIONAMENTOS
' ─────────────────────────────

' Herança (extends)
Pessoa <|-- Cliente
Pessoa <|-- Funcionario

' Realização / Implementação (implements)
Pagavel <|.. PagamentoCartao
Pagavel <|.. PagamentoPix
Pagavel <|.. PagamentoBoleto

' Associações
Cliente "1" --> "0..*" Pedido : realiza
Pedido "1" *-- "1..*" ItemPedido : contém
ItemPedido "0..*" --> "1" Produto : referencia
Pedido "1" --> "1" Pagavel : pago com

@enduml
```

## Relacionamentos

| Símbolo | Tipo       | Descrição                    |
| ------- | ---------- | ---------------------------- |
| `-->`   | Associação | Uma classe usa/conhece outra |
| `*--`   | Composição | Parte essencial do todo      |
| `o--`   | Agregação  | Parte independente do todo   |
| `<\|--` | Herança    | Herda atributos e métodos    |
| `..>`   | Realização | N                            |

## Modificadores de Acesso

|Símbolo|Acesso|
|---|---|
|`+`|público|
|`-`|privado|
|`#`|protegido|
|`~`|pacote|

## Multiplicidades

| Notação | Significado   |
| ------- | ------------- |
| `1`     | Exatamente um |
| `0..*`  | Zero ou mais  |
| `1..*`  | Um ou mais    |
| `0..1`  | Zero ou um    |