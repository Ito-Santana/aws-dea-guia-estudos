---

title: S3 - Criptografia de Objetos
layout: default
description: Criptografia de objetos no Amazon S3 com foco em SSE-S3, SSE-KMS, SSE-C, client-side encryption e criptografia em trânsito
---

# S3 - Criptografia de Objetos

## Visão Geral

Criptografia no `Amazon S3` serve para proteger dados contra acesso indevido.

Existem dois momentos importantes para pensar nisso:

```text
dados em repouso -> quando estão armazenados no S3
dados em trânsito -> quando estão trafegando entre cliente, serviço e S3
```

Para a `DEA-C01`, o foco principal é entender as opções de criptografia em repouso:

* `SSE-S3`;
* `SSE-KMS`;
* `SSE-C`;
* client-side encryption.

E também lembrar que a criptografia em trânsito normalmente usa `HTTPS/TLS`.

Hoje, o S3 já aplica criptografia em repouso por padrão usando `SSE-S3` para novos objetos, mas a prova ainda pode cobrar quando escolher `SSE-KMS` ou outros modelos.

---

## Criptografia em repouso

Criptografia em repouso é a proteção dos dados enquanto eles estão armazenados.

No caso do S3, significa que o objeto fica criptografado no storage.

Exemplo:

```text
arquivo salvo no S3 -> objeto criptografado em repouso
```

As opções principais são:

```text
SSE-S3
SSE-KMS
SSE-C
Client-side encryption
```

A diferença entre elas está principalmente em **quem gerencia as chaves** e **onde a criptografia acontece**.

---

## SSE-S3

`SSE-S3` significa **Server-Side Encryption with Amazon S3 managed keys**.

Aqui, o próprio S3 criptografa o objeto e gerencia as chaves.

É a opção mais simples.

Você envia o objeto, e o S3 cuida da criptografia no lado do servidor.

```text
Cliente -> envia objeto -> S3 criptografa e gerencia as chaves
```

Use `SSE-S3` quando você quer criptografia em repouso sem precisar gerenciar chaves no `AWS KMS`.

Para a prova, guarde:

```text
SSE-S3 = criptografia gerenciada pelo próprio S3
```

É a opção padrão para novos objetos no S3.

---

## SSE-KMS

`SSE-KMS` significa **Server-Side Encryption with AWS KMS keys**.

Aqui, o S3 ainda faz a criptografia no lado do servidor, mas as chaves são gerenciadas pelo `AWS KMS`.

A diferença é que o `KMS` dá mais controle.

Com `SSE-KMS`, você pode ter:

* controle sobre a chave;
* políticas de chave;
* auditoria via `CloudTrail`;
* uso de customer managed keys;
* controle mais forte para compliance.

Exemplo mental:

```text
Cliente -> envia objeto -> S3 criptografa usando chave do KMS
```

Use `SSE-KMS` quando o cenário pede mais controle, auditoria ou governança sobre as chaves.

Para a prova, guarde:

```text
SSE-KMS = S3 criptografa, KMS gerencia a chave
```

A AWS descreve `SSE-KMS` como a integração do S3 com o `AWS KMS`, permitindo maior controle sobre as chaves usadas na criptografia.

---

## S3 Bucket Keys

Quando você usa `SSE-KMS`, muitas operações podem gerar chamadas ao `AWS KMS`.

Em buckets com muito volume, isso pode impactar custo.

`S3 Bucket Keys` ajudam a reduzir chamadas ao KMS e, por consequência, reduzir custo de uso do `SSE-KMS`.

Para a prova, não precisa aprofundar muito.

Guarde assim:

```text
S3 Bucket Key = ajuda a reduzir custo de SSE-KMS
```

A AWS informa que S3 Bucket Keys podem reduzir custos de requisições ao KMS para objetos criptografados com `SSE-KMS`.

---

## SSE-C

`SSE-C` significa **Server-Side Encryption with Customer-Provided Keys**.

Nesse modelo, a criptografia ainda acontece no lado do servidor, mas quem fornece a chave é o cliente.

Ou seja:

```text
Cliente fornece a chave -> S3 usa a chave para criptografar/decriptografar -> S3 não armazena a chave
```

Isso dá mais responsabilidade para quem está usando o S3.

Se você perder a chave, não consegue recuperar o objeto.

Para a prova, guarde:

```text
SSE-C = cliente fornece e gerencia a chave
```

É uma opção mais específica e menos comum em arquiteturas modernas. Inclusive, a AWS passou a bloquear `SSE-C` por padrão em novos buckets de uso geral, exigindo configuração explícita para permitir esse tipo de criptografia.

---

## Client-side encryption

Na **client-side encryption**, a criptografia acontece antes do objeto chegar ao S3.

Ou seja, o cliente criptografa o dado localmente e envia o objeto já criptografado.

```text
Cliente criptografa -> envia para o S3 -> S3 armazena objeto já criptografado
```

Nesse caso, o S3 armazena o dado, mas não é ele que faz a criptografia principal do conteúdo.

Use quando você precisa controlar a criptografia antes dos dados saírem da aplicação ou do ambiente de origem.

Para a prova, guarde:

```text
Client-side encryption = dado já chega criptografado no S3
```

O cuidado aqui é que o gerenciamento de chaves e o processo de descriptografia ficam mais sob responsabilidade da aplicação ou cliente.

---

## Criptografia em trânsito

Criptografia em trânsito protege os dados enquanto eles estão trafegando.

Exemplo:

```text
aplicação -> S3
Athena -> S3
Glue -> S3
cliente -> S3
```

No S3, isso normalmente significa usar `HTTPS` com `TLS`.

A diferença é simples:

```text
HTTP  -> dado trafega sem criptografia
HTTPS -> dado trafega protegido com TLS
```

A AWS documenta que o S3 aceita HTTP e HTTPS, mas recomenda proteger dados em trânsito usando HTTPS/TLS.

Em ambientes seguros, é comum criar uma bucket policy negando acesso sem HTTPS:

```text
Deny se aws:SecureTransport = false
```

Para a prova, guarde:

```text
criptografia em trânsito = HTTPS/TLS
```

---

## Comparação rápida

| Tipo                   | Onde criptografa  | Quem gerencia a chave | Melhor uso                                   |
| ---------------------- | ----------------- | --------------------- | -------------------------------------------- |
| `SSE-S3`               | Servidor/S3       | Amazon S3             | Criptografia simples e padrão                |
| `SSE-KMS`              | Servidor/S3       | AWS KMS               | Mais controle, auditoria e compliance        |
| `SSE-C`                | Servidor/S3       | Cliente               | Cliente quer fornecer a própria chave        |
| Client-side encryption | Cliente           | Cliente/aplicação     | Dado precisa sair da origem já criptografado |
| Em trânsito            | Durante o tráfego | TLS/HTTPS             | Proteger comunicação até o S3                |



---

## Relação com replicação

Criptografia também aparece em cenários de replicação.

Objetos criptografados com `SSE-S3` costumam ser mais simples de replicar.

Com `SSE-KMS`, você precisa garantir permissões corretas para as chaves KMS envolvidas.

Exemplo:

```text
S3 precisa permissão para usar a chave KMS na origem e no destino
```

Para a prova, pense:

```text
replicação + SSE-KMS = atenção extra em permissões KMS
```

A AWS possui documentação específica para replicação de objetos criptografados com `SSE-S3`, `SSE-KMS` e `DSSE-KMS`.

---

## Pegadinhas para a prova

* `SSE-S3` é gerenciado pelo próprio S3.
* `SSE-KMS` usa chaves do `AWS KMS`.
* `SSE-KMS` dá mais controle e auditoria.
* `SSE-C` usa chave fornecida pelo cliente.
* Em `SSE-C`, se perder a chave, perde acesso ao objeto.
* Client-side encryption criptografa antes de enviar ao S3.
* Criptografia em trânsito usa `HTTPS/TLS`.
* Dá para negar acesso sem HTTPS usando `aws:SecureTransport`.
* `SSE-KMS` pode exigir permissões extras em replicação.
* `S3 Bucket Keys` podem reduzir custo em `SSE-KMS`.
* Criptografia não substitui IAM, bucket policy ou controle de acesso.

---

## Quando usar

Use `SSE-S3` quando você quer criptografia simples e gerenciada pelo S3.

Use `SSE-KMS` quando precisa de mais controle, auditoria e compliance.

Use `SSE-C` quando o cliente precisa fornecer e controlar a própria chave.

Use client-side encryption quando o dado precisa ser criptografado antes de chegar ao S3.

Use `HTTPS/TLS` sempre que os dados estiverem trafegando até o S3.

---

## Resumo rápido

Criptografia no S3 pode proteger dados em repouso e em trânsito.

Em repouso:

```text
SSE-S3 -> S3 gerencia
SSE-KMS -> KMS gerencia
SSE-C -> cliente fornece a chave
Client-side encryption -> cliente criptografa antes de enviar
```

Em trânsito:

```text
HTTPS/TLS
```

Para a `DEA-C01`, o mais importante é diferenciar quem gerencia a chave e onde a criptografia acontece.
