---

title: ETL
layout: default
description: Extract, Transform, Load no contexto de pipelines de dados na AWS
---

# ETL

## Visão Geral

ETL significa **Extract, Transform, Load**: extrair, transformar e carregar.

A ideia é pegar dados de uma origem, tratar esses dados e depois gravar o resultado em um destino.

De forma simples:

```text
Dado bruto -> Tratamento -> Dado pronto para consumo
```

---

## Por que isso importa?

Sem ETL, cada time pode acabar limpando e interpretando os dados de um jeito diferente. Um relatório calcula receita de uma forma, outro calcula de outra, e ninguém sabe qual número está certo.

ETL ajuda a criar uma versão mais padronizada e confiável dos dados.

---

## Etapas do ETL

### Extract

É a extração dos dados da origem.

Pode vir de:

* `Amazon RDS`;
* `Amazon DynamoDB`;
* APIs;
* arquivos no `Amazon S3`;
* logs;
* eventos.

A pergunta aqui é:

> De onde o dado vem?

---

### Transform

É onde o dado é tratado.

Aqui você pode:

* corrigir tipos;
* tratar nulos;
* remover duplicidades;
* padronizar datas;
* aplicar regras de negócio;
* fazer joins;
* converter `CSV` para `Parquet`.

Exemplo:

```text
valor = "1500.50"  -> texto
valor = 1500.50    -> número
```

---

### Load

É a carga do dado tratado no destino.

Destinos comuns:

* `Amazon S3`;
* `Amazon Redshift`;
* tabelas para consulta no `Athena`;
* camadas curadas de um data lake.

No ETL clássico, o dado chega ao destino **já tratado**.

---

## Exemplo na AWS

Imagine que arquivos `CSV` de vendas chegam todos os dias no `S3`.

Um job no `AWS Glue` pode:

1. Ler os arquivos brutos;
2. Corrigir tipos;
3. Remover registros inválidos;
4. Padronizar datas;
5. Converter para `Parquet`;
6. Gravar a camada curada no `S3`;
7. Deixar a tabela disponível para consulta no `Athena`.

```mermaid
flowchart LR
    A[CSV bruto no S3] --> B[AWS Glue]
    B --> C[Transformacao]
    C --> D[Parquet curado no S3]
    D --> E[Consulta via Athena]
```

---

## Como aparece na AWS

Na AWS, ETL aparece muito com:

* `AWS Glue`;
* `Amazon S3`;
* `AWS Glue Data Catalog`;
* `Amazon Athena`;
* `Amazon Redshift`;
* `Amazon EMR`;
* `AWS Step Functions`;
* `Amazon EventBridge`.

Para prova, guarde:

> Se a questão fala em ETL gerenciado, serverless e integrado à AWS, pense primeiro em `AWS Glue`.

---

## ETL vs ELT

A diferença é a ordem.

No **ETL**, você transforma antes de carregar:

```text
Extract -> Transform -> Load
```

No **ELT**, você carrega primeiro e transforma depois:

```text
Extract -> Load -> Transform
```

Forma simples de lembrar:

* **ETL**: limpo antes de entregar;
* **ELT**: entrego primeiro e limpo depois.

ETL faz sentido quando o dado precisa chegar mais controlado ao destino.
ELT faz sentido quando o destino analítico, como um warehouse, consegue transformar depois.

---

## ETL não é só ingestão

Ingestão é apenas trazer o dado para dentro da arquitetura.

Exemplo:

```text
Copiar um arquivo bruto para o S3
```

Isso é ingestão.

ETL envolve transformação:

```text
Ler o arquivo, limpar, aplicar regra, converter para Parquet e salvar em uma camada curada
```

Então:

> Toda ETL começa com ingestão, mas nem toda ingestão é ETL.

---

## Quando usar

Use ETL quando:

* o dado precisa ser tratado antes do consumo;
* existem regras de negócio antes da carga final;
* você quer criar uma camada curada;
* vários times precisam consumir a mesma versão confiável.

---

## Quando não usar

ETL pode não ser o melhor caminho quando:

* você só quer aterrissar dado bruto rapidamente;
* o destino vai fazer as transformações depois;
* o padrão da arquitetura é ELT;
* a transformação é mínima.

---

## Resumo rápido

ETL é o processo de extrair dados, transformar e carregar o resultado em um destino.

Ele existe porque dado bruto quase nunca chega pronto para consumo.

Na AWS, o principal serviço associado a ETL é o `AWS Glue`.

Para a prova, foque em três coisas: a ordem do ETL, a diferença para ELT e quando usar Glue.

---
