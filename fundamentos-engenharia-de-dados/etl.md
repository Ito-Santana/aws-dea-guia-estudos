---
title: ETL
layout: default
description: Conceito básico de ETL e sua relação com pipelines de dados na AWS
---

# ETL

**ETL** significa **Extract, Transform, Load**.

É uma forma bem comum de pensar o fluxo dos dados: primeiro você extrai da origem, depois trata, e por fim carrega para um destino que vai ser usado para análise ou consumo.

Na prática, ETL aparece muito em engenharia de dados porque os dados quase nunca chegam prontos. Sempre tem ajuste de tipo, limpeza, padronização, remoção de duplicidade ou alguma regra de negócio no meio.

---

## As 3 etapas

### Extract

É a parte de pegar os dados da origem.

A origem pode ser:

* banco relacional;
* API;
* arquivo em bucket;
* sistema legado;
* fila ou evento.

Na AWS, isso pode vir de fontes como **RDS**, **DynamoDB**, **S3** ou uma aplicação externa.

### Transform

É onde o dado é tratado.

Aqui entram tarefas como:

* converter formatos;
* corrigir tipos;
* remover registros ruins;
* aplicar regras de negócio;
* juntar tabelas;
* criar colunas novas.

Na AWS, isso costuma ser feito com **AWS Glue**, **Amazon EMR** ou até com SQL em **Redshift** e **Athena**, dependendo do caso.

### Load

É o momento de gravar o dado no destino final.

Esse destino pode ser um:

* data warehouse;
* data lake;
* tabela analítica;
* camada curada de um pipeline.

Em AWS, o destino costuma ser **Amazon S3** ou **Amazon Redshift**.

### Fluxo simples

<div class="mermaid">
flowchart LR
    A[Origem] --> B[Extract]
    B --> C[Transform]
    C --> D[Load]
    D --> E[Destino]
</div>

---

## Quando usar

ETL faz sentido quando você quer chegar em dados mais organizados antes de disponibilizar para consumo.

É muito usado quando:

* o dado de origem vem bagunçado;
* existe regra de negócio forte;
* o destino precisa ser mais confiável para BI e análise;
* você quer controlar melhor o que entra e o que sai.

---

## Resumo rápido

Se eu simplificar:

* **Extract**: pega o dado.
* **Transform**: trata o dado.
* **Load**: grava o dado no destino.

Na AWS, ETL aparece bastante com **Glue**, **S3**, **Redshift**, **Athena** e **EMR**.
