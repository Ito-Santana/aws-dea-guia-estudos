---
title: S3 - Introdução
layout: default
description: Introdução ao Amazon S3 com foco em conceito e regras básicas de nomeação de buckets
---

# S3 - Introdução

O **Amazon S3** é o serviço de armazenamento de objetos da AWS.

Na prática, ele serve para guardar arquivos e dados de forma simples, escalável e bem durável. Ele é um dos serviços mais importantes da AWS porque aparece em muita coisa: data lake, backup, logs, arquivos brutos, dados curados, estáticos de site e até integração entre serviços.

O jeito mais simples de pensar no S3 é este:

* você cria um **bucket**;
* coloca objetos dentro dele;
* organiza os arquivos por prefixo;
* define permissões, criptografia e ciclo de vida conforme a necessidade.

---

## Bucket e objeto

No S3, o bucket é o contêiner lógico.

O objeto é o arquivo que fica dentro dele. Esse objeto pode ser um CSV, JSON, Parquet, imagem, documento, log ou qualquer outro tipo de arquivo.

Exemplo mental:

* bucket: `dados-vendas`
* objeto: `2025/06/pedidos.csv`

---

## Onde o S3 entra no dia a dia

O S3 costuma ser a base de muita arquitetura de dados na AWS porque ele funciona bem como repositório central.

Ele aparece em cenários como:

* data lake;
* landing zone de ingestão;
* backup;
* arquivos para análise;
* dados curados para consumo;
* arquivos estáticos;
* compartilhamento entre serviços.

---

## Regras vigentes de nomeação de bucket

A AWS mantém regras bem específicas para nome de bucket. As principais, hoje, são estas:

* o nome precisa ter entre **3 e 63 caracteres**;
* só pode usar **letras minúsculas**, números, ponto (`.`) e hífen (`-`);
* o nome precisa começar e terminar com **letra ou número**;
* não pode ter **dois pontos seguidos**;
* não pode ter formato de **endereço IP**;
* não pode começar com `xn--`;
* não pode começar com `sthree-`;
* não pode começar com `amzn-s3-demo-`;
* não pode terminar com `-s3alias`;
* não pode terminar com `--ol-s3`;
* não pode terminar com `.mrap`;
* não pode terminar com `--x-s3`;
* não pode terminar com `--table-s3`;
* não pode terminar com `-an`, a não ser quando você estiver criando bucket no **account regional namespace**;
* se usar **S3 Transfer Acceleration**, o nome não pode ter ponto (`.`).

Além disso:

* bucket S3 existe em **namespace global**;
* o nome precisa ser único dentro da partição;
* depois que o bucket é criado, você não muda o nome nem a região;
* não é uma boa ideia colocar informação sensível no nome do bucket, porque ele aparece na URL.

### Exemplo de nome válido

```text
meu-time-dados-2025
```

### Exemplo de nome ruim

```text
Meu_Time_Dados
```

Esse segundo exemplo não vale porque tem letra maiúscula e underscore.

---

## Account regional namespace

A AWS também permite criar buckets no **account regional namespace**.

Isso é útil quando você quer nomes previsíveis e quer garantir que só a sua conta possa usar aquele nome.

O formato geral é:

```text
bucket-name-prefix-accountId-region-an
```

Exemplo:

```text
dados-vendas-111122223333-us-west-2-an
```

---

## Resumo rápido

Se eu simplificar:

* S3 é armazenamento de objetos;
* bucket é o contêiner;
* objeto é o arquivo;
* nome de bucket tem regra rígida;
* o S3 costuma ser a base de muita arquitetura de dados na AWS.
