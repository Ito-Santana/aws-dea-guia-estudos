---

title: DynamoDB - Segurança
layout: default
description: Segurança no Amazon DynamoDB com foco em IAM, criptografia, VPC endpoints, backups e boas práticas
---

# DynamoDB - Segurança

## Visão Geral

Segurança no `Amazon DynamoDB` envolve controlar quem pode acessar a tabela, proteger os dados e garantir recuperação em caso de erro.


---

## IAM

O controle de acesso ao DynamoDB é feito principalmente com `IAM`.

Com IAM, você define quais usuários, roles ou serviços podem executar ações na tabela.

Exemplos de ações:

```text
dynamodb:GetItem
dynamodb:PutItem
dynamodb:UpdateItem
dynamodb:DeleteItem
dynamodb:Query
dynamodb:Scan
```


---

## Permissões por tabela e índice

As permissões podem ser aplicadas em recursos específicos.

Exemplo:

```text
permitir acesso apenas à tabela Pedidos
permitir consulta em um GSI específico
negar Scan em produção
```

Isso ajuda a aplicar o princípio do menor privilégio.

Ou seja, cada aplicação ou pessoa recebe somente as permissões necessárias.


---

## Criptografia em repouso

O DynamoDB criptografa os dados em repouso.

Isso significa que os dados armazenados na tabela ficam protegidos no storage.

A criptografia usa chaves do `AWS KMS`.

A AWS informa que todos os dados de usuário armazenados no DynamoDB são criptografados em repouso, incluindo tabelas, índices, streams e backups.

Você pode usar:

| Tipo de chave        | Ideia                                     |
| -------------------- | ----------------------------------------- |
| AWS owned key        | Chave gerenciada pela AWS                 |
| AWS managed key      | Chave gerenciada pela AWS para o serviço  |
| Customer managed key | Chave criada e controlada por você no KMS |


---

## Criptografia em trânsito

Criptografia em trânsito protege os dados enquanto eles trafegam entre a aplicação e o DynamoDB.

O DynamoDB usa `HTTPS/TLS` para proteger essa comunicação.

A AWS documenta que, por padrão, comunicações com DynamoDB usam HTTPS, protegendo o tráfego com SSL/TLS.

---

## VPC Endpoint

Por padrão, uma aplicação dentro de uma VPC pode acessar DynamoDB usando endpoints públicos da AWS.

Mas você pode usar `VPC Endpoint` para acessar DynamoDB de forma privada pela rede da AWS.

Isso evita depender de internet gateway ou NAT para esse acesso.

A AWS oferece VPC endpoints para DynamoDB, incluindo gateway endpoints e interface endpoints com AWS PrivateLink.

---

## Backup e PITR

Segurança também envolve recuperação.

No DynamoDB, dois recursos importantes são:

| Recurso          | Ideia                              |
| ---------------- | ---------------------------------- |
| Backup on-demand | Backup manual da tabela            |
| PITR             | Recuperação para um ponto no tempo |

`PITR` significa `Point-in-Time Recovery`.

Ele permite recuperar a tabela para um ponto específico dentro da janela suportada.

A AWS informa que o PITR fornece backups contínuos gerenciados pelo DynamoDB, com recuperação de até 35 dias.

---

## Resumo rápido

Segurança no DynamoDB envolve acesso, criptografia, rede e recuperação.

Para lembrar:

```text
IAM -> permissões
KMS -> criptografia em repouso
TLS -> criptografia em trânsito
VPC Endpoint -> acesso privado
PITR -> recuperação

```
