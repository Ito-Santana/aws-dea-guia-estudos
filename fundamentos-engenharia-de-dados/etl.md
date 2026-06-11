---
title: ETL
layout: default
description: Conceito básico de ETL e sua relação com pipelines de dados na AWS
---

# ETL

**ETL** quer dizer **Extract, Transform, Load**.

É um jeito de organizar o caminho do dado desde a origem até o destino final. Em quase todo projeto de dados, o dado não chega pronto. Ele vem com campo vazio, formato errado, tipo inconsistente, duplicidade ou alguma regra de negócio que precisa ser aplicada antes do consumo.

Por isso o ETL é tão comum: ele coloca ordem no fluxo.

---

## Como pensar no ETL

O fluxo é simples de entender:

1. você tira os dados da origem;
2. você trata o que precisa ser ajustado;
3. você grava o resultado em algum lugar pronto para uso.

### Fluxo

<div class="mermaid">
flowchart LR
    A[Origem] --> B[Extract]
    B --> C[Transform]
    C --> D[Load]
    D --> E[Destino]
</div>

---

## Extract

Aqui você pega os dados da fonte.

A fonte pode ser:

* banco relacional;
* API;
* arquivo;
* sistema legado;
* fila;
* evento.

Na AWS, isso aparece bastante com **RDS**, **DynamoDB**, **S3** e outras origens externas.

Nessa etapa, o foco não é tratar o dado. É só trazer ele com segurança e consistência.

---

## Transform

Essa é a parte em que o dado ganha forma.

É aqui que entram as tarefas que mais aparecem no dia a dia:

* trocar tipo de coluna;
* padronizar datas;
* remover duplicidade;
* tratar nulos;
* aplicar regra de negócio;
* juntar tabelas;
* criar colunas derivadas;
* filtrar o que não presta.

Essa etapa costuma ser a mais trabalhosa. É também a parte que mais separa um dado bruto de um dado útil.

Na AWS, a transformação pode acontecer em **AWS Glue**, **Amazon EMR**, **Athena** ou **Redshift**, dependendo da arquitetura.

---

## Load

Depois do tratamento, você carrega o dado no destino.

Esse destino pode ser:

* um data lake;
* um data warehouse;
* uma tabela curada;
* uma camada pronta para consumo analítico.

Na AWS, isso normalmente termina em **S3** ou **Redshift**.

O ponto aqui é simples: o dado sai da origem, passa por tratamento e chega num lugar mais confiável para consulta.

---

## ETL na prática

ETL faz sentido quando você quer entregar dado mais organizado antes do consumo.

Ele é muito útil quando:

* a origem vem despadronizada;
* existe regra de negócio clara;
* o destino precisa ser confiável;
* o time quer controlar melhor o que entra e o que sai;
* a camada analítica precisa de consistência.

Se eu resumir de forma bem direta:

* **Extract**: pega;
* **Transform**: trata;
* **Load**: grava.

---

## Resumo rápido

ETL é o fluxo básico de dados saindo da origem, sendo tratado e chegando ao destino.

Na AWS, você vai ver isso muito com **Glue**, **S3**, **Redshift**, **Athena** e **EMR**.
