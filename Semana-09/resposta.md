# Atividade semana 09

## PIM (Platform Independent Model)

- Larissa
- Erika
- Talita

## Diagrama de Sequencia

```mermaid

sequenceDiagram
    actor Usuario as Usuário
    participant Frontend as Interface (Frontend)
    participant Controller as Controller de Pedidos
    participant ServicoPagamento as Serviço de Pagamento
    participant Operadora as Operadora de Cartão
    participant Database as Banco de Dados

    Usuario ->> Frontend: Clica em "Finalizar"
    Frontend ->> Controller: Envia dados do pedido
    Controller ->> ServicoPagamento: Solicita validação de pagamento
    ServicoPagamento ->> Operadora: Valida pagamento
    Operadora -->> ServicoPagamento: Retorna resultado da validação

    alt Pagamento aprovado
        Controller ->> Database: Atualiza status do pedido
        Controller -->> Usuario: Confirmação de pedido finalizado
    else Pagamento recusado
        Controller -->> Usuario: Notifica falha no pagamento
    end

```

## Diagrama de classe

```mermaid

%%{init: {"layout": "elk"}}%%
classDiagram
    direction LR
    
    class Cliente {
        +String nome
        +String contato
    }

    class Pedido {
        +Date data
        +String status
    }

    class ItemPedido {
        +int quantidade
        +float preco
    }

    class Produto {
        +String descricao
        +float precoUnitario
    }

    Cliente "1" --> "0..*" Pedido : faz
    Pedido "1" --> "1..*" ItemPedido : contém
    ItemPedido "*" --> "1" Produto : refere-se a

```
## Diagrama de Estado

```mermaid

stateDiagram-v2
    direction LR

  %%{init: {"config": {"layout": "elk"}}}%%
  [*] --> Pendente : carrinho fechado
  Pendente --> Pago : pagamento confirmado
  Pago --> Enviado : produto sai do estoque
  Enviado --> Entregue : entrega confirmada
  Pendente --> Cancelado : cancelamento
  Pago --> Cancelado : estorno
  Entregue --> [*]
  Cancelado --> [*]

  classDef normal stroke:#4ade80,fill:#f0fdf4
  classDef terminal stroke:#f87171,fill:#fef2f2
  class Pendente,Pago,Enviado normal
  class Entregue,Cancelado terminal

  ```

