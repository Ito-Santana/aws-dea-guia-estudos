---

title: DynamoDB - Introdução
layout: default
description: Introdução ao Amazon DynamoDB com foco em NoSQL, tabelas, itens, atributos, chaves e cenários comuns na AWS DEA-C01
---

# DynamoDB - Introdução

## Visão Geral

`Amazon DynamoDB` é um banco de dados `NoSQL` totalmente gerenciado pela AWS.

Diferente de bancos relacionais, como `PostgreSQL` ou `MySQL`, o DynamoDB não trabalha com tabelas relacionais cheias de joins. Ele trabalha com tabelas, itens e atributos.

`NoSQL` é um termo usado para bancos que não seguem o modelo relacional tradicional.

No caso do DynamoDB, o modelo é de chave-valor e documento.

Isso significa que os dados são acessados principalmente por chaves.

Exemplo:

```text
customer_id = 123
```

A aplicação usa essa chave para buscar rapidamente o item correspondente.

O DynamoDB também permite atributos flexíveis. Nem todos os itens da tabela precisam ter exatamente os mesmos campos.

Exemplo:

```json
{
  "customer_id": "123",
  "nome": "Ana",
  "plano": "premium"
}
```

Outro item da mesma tabela poderia ter atributos diferentes:

```json
{
  "customer_id": "456",
  "nome": "Bruno",
  "cidade": "Recife",
  "ultimo_login": "2026-06-12"
}
```

Essa flexibilidade é uma das diferenças em relação a bancos relacionais.

---

## Tabela

No DynamoDB, uma tabela é onde os itens ficam armazenados.

Exemplo:

```text
Tabela: Clientes
```

Dentro da tabela, você armazena itens.

```text
Cliente 123
Cliente 456
Cliente 789
```

A tabela precisa ter uma chave primária definida.

Essa chave é usada para identificar e acessar os itens de forma eficiente.

---

## Item

Um item é um registro dentro da tabela.

Ele é parecido com uma linha em um banco relacional, mas com mais flexibilidade.

Exemplo de item:

```json
{
  "customer_id": "123",
  "nome": "Ana",
  "plano": "premium",
  "status": "ativo"
}
```

Cada item é formado por atributos.

Para a prova, pense assim:

```text
item = registro dentro da tabela
```

---

## Atributo

Atributo é um campo dentro de um item.

No exemplo abaixo:

```json
{
  "customer_id": "123",
  "nome": "Ana",
  "plano": "premium"
}
```

Os atributos são:

```text
customer_id
nome
plano
```

Um ponto importante: o DynamoDB é mais flexível que um banco relacional. Alguns atributos podem existir em um item e não existir em outro.

Mas isso não significa que você pode modelar sem pensar. No DynamoDB, a modelagem depende muito de como a aplicação vai consultar os dados.

---

## Chave primária

A chave primária identifica os itens da tabela.

No DynamoDB, ela pode ser de dois tipos:

| Tipo                     | Como funciona                                      |
| ------------------------ | -------------------------------------------------- |
| Partition key            | Usa apenas uma chave                               |
| Partition key + sort key | Usa uma chave de partição e uma chave de ordenação |

---

## Partition Key

<img width="800" height="486" alt="image" src="https://github.com/user-attachments/assets/3a683c89-9197-4b38-ab3f-821fce34c235" />

A `partition key` é a chave usada para distribuir e localizar os dados.

Exemplo:

```text
customer_id
```

Se a tabela usa apenas `customer_id` como chave primária, cada item precisa ter um `customer_id` único.

Exemplo:

```text
customer_id = 123
```

Para a prova, guarde:

```text
partition key = chave principal usada para distribuir e acessar os dados
```

Uma boa partition key deve distribuir bem os acessos. Se muitos acessos caem sempre no mesmo valor, pode haver concentração de carga.

---

## Sort Key

A `sort key` é usada junto com a partition key.

Ela permite armazenar vários itens com a mesma partition key, diferenciando-os pela ordenação.

Exemplo:

```text
partition key: customer_id
sort key: order_id
```

Isso permite ter vários pedidos para o mesmo cliente:

```text
customer_id = 123 | order_id = A001
customer_id = 123 | order_id = A002
customer_id = 123 | order_id = A003
```

Esse modelo é útil quando você quer consultar vários itens relacionados a uma mesma entidade.

Exemplo:

```text
buscar todos os pedidos do cliente 123
```

Para a prova:

```text
sort key = organiza itens dentro da mesma partition key
```

---

## Como aparece na AWS

DynamoDB aparece em cenários como:

* aplicações serverless;
* aplicações com grande escala;
* dados de sessão;
* eventos simples por usuário;


---
