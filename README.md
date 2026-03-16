# Desafio-e-comerce-ci-ncia-de-dados-

utilizarei a linguagem Mermaid.js, que permite criar diagramas de Entidade-Relacionamento (ER) de forma textual e visual, facilitando a identificação clara de PKs (Primary Keys) e FKs (Foreign Keys) dentro do esquema lógico/conceitual.

Este modelo foca no fluxo essencial: Cliente -> Pedido -> Produto, com as devidas tabelas de ligação para suportar relacionamentos N:N.
Esquema Conceitual de E-commerce (Código Mermaid)
mermaid
erDiagram
    CLIENTE ||--o{ PEDIDO : "realiza"
    PEDIDO ||--|{ ITEM_PEDIDO : "contem"
    PRODUTO ||--|{ ITEM_PEDIDO : "incluido em"
    PEDIDO ||--|| PAGAMENTO : "gera"

    CLIENTE {
        int id_cliente PK
        string nome
        string email
        string cpf_cnpj
        string endereco
    }

    PEDIDO {
        int id_pedido PK
        int id_cliente FK
        datetime data_criacao
        float valor_total
        string status
    }

    ITEM_PEDIDO {
        int id_item PK
        int id_pedido FK
        int id_produto FK
        int quantidade
        float preco_unitario
    }

    PRODUTO {
        int id_produto PK
        string nome
        string descricao
        float preco
        int estoque
    }

    PAGAMENTO {
        int id_pagamento PK
        int id_pedido FK
        string forma_pagamento
        string status_pagamento
        datetime data_pagamento
    }
Use o código com cuidado.

Pontos-Chave da Modelagem:
Chaves Primárias (PK): Cada entidade possui um identificador único (ex: id_cliente, id_pedido), garantindo a integridade referencial.

Chaves Estrangeiras (FK):

PEDIDO referencia CLIENTE para saber quem comprou.
ITEM_PEDIDO atua como a tabela de ligação (N:N) entre PEDIDO e PRODUTO, carregando as chaves de ambos.
PAGAMENTO referencia o PEDIDO para garantir que cada transação financeira esteja atrelada a uma venda.

Cardinalidade:

Um Cliente pode ter zero ou vários pedidos.
Um Pedido deve ter pelo menos um item e pertence a apenas um cliente.
Um Produto pode aparecer em muitos itens de pedidos diferentes. 
