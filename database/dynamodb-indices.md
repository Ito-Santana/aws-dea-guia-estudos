---

title: DynamoDB - Índices
layout: default
description: Índices no Amazon DynamoDB com foco em LSI, GSI e padrões de consulta
---

# DynamoDB - Índices

## Visão Geral

No `DynamoDB`, índice é uma forma de consultar a tabela por outro caminho.

A tabela principal sempre tem uma chave primária. Mas nem toda consulta da aplicação vai usar essa chave.

Exemplo:

```text
Tabela Pedidos
partition key: customer_id
sort key: order_id
```

Essa estrutura funciona bem para buscar pedidos de um cliente.

Mas se a aplicação precisar buscar pedidos por `status`, a chave principal não resolve tão bem.

Nesse caso, um índice pode ser usado para criar outro padrão de acesso sem depender de `Scan`.

---

## Por que usar índices?

O DynamoDB é eficiente quando você consulta usando chaves.

Quando você precisa buscar por outro atributo com frequência, criar um índice costuma ser melhor do que varrer a tabela inteira.

---

## Tipos de índice

O DynamoDB tem dois tipos principais:

| Índice | Ideia                                             |
| ------ | ------------------------------------------------- |
| `LSI`  | Mesma partition key da tabela, mas outra sort key |
| `GSI`  | Pode usar outra partition key e outra sort key    |

---

## LSI

`LSI` significa `Local Secondary Index`.

Ele mantém a mesma `partition key` da tabela principal, mas usa uma `sort key` diferente.

Exemplo:

```text
Tabela principal:
partition key: customer_id
sort key: order_id

LSI:
partition key: customer_id
sort key: order_date
```

Isso permite consultar os pedidos do mesmo cliente, mas ordenando ou filtrando por data.

Use `LSI` quando a consulta ainda começa pela mesma entidade.

Exemplos:

```text
pedidos do cliente por data
eventos do usuário por timestamp
compras do cliente por valor
```

**OBS: LSI precisa ser criado junto com a tabela.**


---

## GSI

`GSI` significa `Global Secondary Index`.

Ele permite consultar a tabela usando outra chave.

Exemplo:

```text
Tabela principal:
partition key: customer_id
sort key: order_id

GSI:
partition key: status
sort key: order_date
```

Agora a aplicação consegue buscar pedidos por `status`.

Use `GSI` quando existe outro padrão de acesso importante.

Exemplos:

```text
buscar usuário por email
buscar pedidos por status
buscar produtos por categoria
buscar eventos por device_id
```

**OBS: Diferente do `LSI`, o `GSI` pode ser criado depois da tabela.**

---

## LSI vs GSI

| Característica | LSI                                      | GSI                      |
| -------------- | ---------------------------------------- | ------------------------ |
| Partition key  | Igual à tabela                           | Pode ser diferente       |
| Sort key       | Diferente                                | Pode ser diferente       |
| Criação        | Junto com a tabela                       | Pode ser depois          |
| Uso comum      | Outra ordenação dentro da mesma entidade | Outro padrão de consulta |

Resumo:

```text
LSI = mesma partition key, outra sort key
GSI = outra chave de consulta
```

---

## Índices e custo

Índices ajudam na leitura, mas têm custo.

Quando um item é escrito ou atualizado na tabela, os índices relacionados também podem precisar ser atualizados.

Então, mais índices significam:

* mais armazenamento;
* mais custo de escrita;
* mais manutenção interna;
* mais cuidado na modelagem.

Por isso, o ideal é criar índice quando existe um padrão de consulta claro.

---
