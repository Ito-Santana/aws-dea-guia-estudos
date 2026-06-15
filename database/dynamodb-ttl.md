---

title: DynamoDB - TTL
layout: default
description: Introdução simples ao Time to Live no Amazon DynamoDB para expiração automática de itens
---

# DynamoDB - TTL

## Visão Geral

`TTL` significa `Time to Live`.

No `DynamoDB`, TTL serve para expirar itens automaticamente depois de uma data/hora definida.

---

## Como funciona

Você escolhe um atributo da tabela para representar a expiração.

Exemplo:

```json
{
  "session_id": "abc123",
  "user_id": "789",
  "expires_at": 1767225600
}
```

Nesse exemplo, `expires_at` seria o atributo usado pelo TTL.

O valor precisa estar em formato `epoch time`, em segundos.

```text
TTL = timestamp de expiração em segundos
```

Quando o horário chega, o item fica elegível para exclusão.

---

## TTL não é exclusão imediata

Esse é o ponto mais importante.

TTL não significa que o item será apagado exatamente no segundo da expiração.

O item fica elegível para remoção, e o DynamoDB apaga de forma assíncrona.

Então, por um tempo, o item expirado ainda pode aparecer em:

```text
GetItem
Query
Scan
```


---

## Quando usar TTL

Use TTL para dados que naturalmente perdem validade.

Exemplos:

* sessões de usuário;
* tokens temporários;
* carrinhos abandonados;
* códigos de verificação;
* eventos temporários;
* cache de aplicação;
* dados que só precisam existir por alguns dias.

---

## TTL e custo

TTL ajuda a controlar crescimento da tabela.

Se itens antigos não têm mais valor, removê-los automaticamente evita acúmulo desnecessário.

Isso pode ajudar em:

* reduzir armazenamento;
* manter a tabela mais limpa;
* evitar processos manuais de limpeza.

Mas lembre: enquanto o item expirado ainda não foi removido, ele ainda conta para armazenamento e pode aparecer em leituras.

---

## TTL e Streams

Quando um item é removido por TTL, essa remoção pode aparecer no `DynamoDB Streams`.

Isso permite reagir à exclusão.

Exemplo:

```text
item expira no DynamoDB
-> evento aparece no Streams
-> Lambda arquiva informação no S3
```

Esse padrão pode ser usado quando você quer limpar a tabela, mas ainda manter um histórico em outro lugar. A AWS mostra esse uso com TTL, Streams e Lambda para arquivar itens expirados.

---

## TTL vs DeleteItem

| Recurso      | Ideia                                     |
| ------------ | ----------------------------------------- |
| `TTL`        | Remove automaticamente depois de um tempo |
| `DeleteItem` | Remove quando a aplicação manda deletar   |

Use `DeleteItem` quando a exclusão precisa acontecer agora.

Use `TTL` quando a exclusão pode acontecer automaticamente depois da expiração.

---


