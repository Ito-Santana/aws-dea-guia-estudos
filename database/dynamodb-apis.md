---

title: DynamoDB - APIs de Dados
layout: default
description: APIs principais do Amazon DynamoDB para escrita, leitura, exclusão e operações em lote
---

# DynamoDB - APIs de Dados

## Visão Geral

No `Amazon DynamoDB`, a aplicação interage com os dados usando APIs.

Essas APIs servem para fazer operações como:

```text
criar item
atualizar item
ler item
consultar itens
varrer tabela
excluir item
executar operações em lote
```


---

## Escrita de dados

As principais APIs de escrita são:

| API              | O que faz                                   |
| ---------------- | ------------------------------------------- |
| `PutItem`        | Cria um item ou substitui um item existente |
| `UpdateItem`     | Atualiza atributos de um item               |
| `BatchWriteItem` | Escreve ou exclui vários itens em lote      |

---

## PutItem

`PutItem` cria um novo item na tabela.

Mas existe um ponto de atenção: se já existir um item com a mesma chave primária, ele pode ser substituído.

Exemplo:

```text
criar cliente customer_id = 123
```

Se outro item com `customer_id = 123` já existir, o novo item pode sobrescrever o antigo.

Para lembrar:

```text
PutItem = inserir item completo
```

---

## UpdateItem

`UpdateItem` altera atributos de um item existente.

Ele é útil quando você não quer substituir o item inteiro.

Exemplo:

```text
alterar status do pedido para ENTREGUE
```

Ou:

```text
incrementar contador de visualizações
```

Para lembrar:

```text
UpdateItem = atualizar parte do item
```

---

## Leitura de dados

As principais APIs de leitura são:

| API       | O que faz                                                |
| --------- | -------------------------------------------------------- |
| `GetItem` | Busca um item pela chave primária                        |
| `Query`   | Busca itens usando partition key e, se existir, sort key |
| `Scan`    | Varre a tabela ou índice                                 |

---

## GetItem

`GetItem` é usado quando você sabe exatamente a chave do item.

Exemplo:

```text
buscar cliente com customer_id = 123
```

Ele é direto e eficiente, porque usa a chave primária.

Para lembrar:

```text
GetItem = buscar um item pela chave
```

---

## Query

`Query` é usado para buscar itens por `partition key`.

Se a tabela tiver `sort key`, você também pode usar condições sobre ela.

Exemplo:

```text
buscar todos os pedidos do cliente 123
```

Modelo da tabela:

```text
partition key: customer_id
sort key: order_id
```

Nesse caso, a `Query` consegue encontrar os pedidos daquele cliente de forma eficiente.

Para lembrar:

```text
Query = busca eficiente usando chave
```

---

## Scan

`Scan` lê todos os itens de uma tabela ou índice.

Ele é mais pesado porque varre os dados.

Exemplo:

```text
listar todos os clientes da tabela
```

O problema é que, em tabelas grandes, isso pode consumir muita capacidade e ser lento.

Para a prova, cuidado:

```text
Scan = varre tudo, geralmente é menos eficiente
```

Se a questão pedir a forma mais eficiente de buscar dados por chave, normalmente a resposta não é `Scan`.

---

## GetItem vs Query vs Scan

| Operação  | Quando usar                                      | Eficiência      |
| --------- | ------------------------------------------------ | --------------- |
| `GetItem` | Quando sabe a chave exata do item                | Muito eficiente |
| `Query`   | Quando busca por partition key e talvez sort key | Eficiente       |
| `Scan`    | Quando precisa varrer a tabela                   | Menos eficiente |

Resumo simples:

```text
GetItem -> um item específico
Query   -> itens por chave
Scan    -> varrer tabela
```

---

## Exclusão de dados

A principal API para exclusão é:

```text
DeleteItem
```

`DeleteItem` remove um item da tabela usando a chave primária.

Exemplo:

```text
deletar customer_id = 123
```

Para lembrar:

```text
DeleteItem = excluir item pela chave
```

Também é possível usar condições para evitar deletar algo por engano.

Exemplo mental:

```text
deletar pedido apenas se status = CANCELADO
```

---

## Operações em lote

Operações em lote servem para trabalhar com vários itens em uma única chamada.

As principais são:

| API              | O que faz                   |
| ---------------- | --------------------------- |
| `BatchGetItem`   | Lê vários itens             |
| `BatchWriteItem` | Cria ou exclui vários itens |

---

## BatchGetItem

`BatchGetItem` busca vários itens de uma vez.

É útil quando você já sabe as chaves dos itens que quer buscar.

Exemplo:

```text
buscar os clientes 123, 456 e 789
```

Para lembrar:

```text
BatchGetItem = vários GetItem juntos
```

---

## BatchWriteItem

`BatchWriteItem` permite fazer várias operações de escrita em lote.

Ele pode fazer:

```text
PutItem
DeleteItem
```

Mas atenção: ele não faz `UpdateItem`.

Para atualizar vários itens, você precisa usar outras estratégias, como várias chamadas de `UpdateItem` ou transações, dependendo do cenário.

Para lembrar:

```text
BatchWriteItem = put e delete em lote, mas não update
```

---

## Operações condicionais

Algumas APIs aceitam condições.

Isso ajuda a evitar alterações erradas.

Exemplo:

```text
criar item apenas se ele ainda não existir
```

Ou:

```text
atualizar pedido apenas se o status atual for PENDENTE
```

Isso é útil para proteger a lógica da aplicação.

Para a prova, guarde:

```text
condition expression = só executa se a condição for verdadeira
```
---
