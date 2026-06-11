---
title: ETL
layout: default
description: Conceito básico de ETL e sua relação com pipelines de dados na AWS
---

# ETL

**ETL** quer dizer **Extract, Transform, Load**.

É um jeito de organizar o caminho do dado desde a origem até o destino. Na prática, o dado quase nunca chega pronto. Ele vem com campo faltando, tipo errado, valor duplicado, data fora do padrão ou alguma regra de negócio que ainda precisa ser aplicada.

Por isso ETL é tão básico em engenharia de dados: ele coloca ordem no fluxo.

---

## Como pensar no ETL

Uma forma simples de enxergar isso é:

1. pegar o dado da origem;
2. tratar o que precisa ser corrigido;
3. gravar o resultado em um destino mais confiável.

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

É a etapa de extrair o dado da fonte.

A fonte pode ser:

* banco relacional;
* API;
* arquivo;
* sistema legado;
* fila;
* evento.

Na AWS, isso pode vir de **RDS**, **DynamoDB**, **S3** ou fontes externas.

O foco aqui é trazer o dado para dentro do pipeline sem alterar o significado dele.

---

## Transform

Essa é a parte em que o dado ganha forma.

Aqui entram as tarefas mais comuns do dia a dia:

* trocar tipo de coluna;
* padronizar datas;
* remover duplicidade;
* tratar nulos;
* aplicar regra de negócio;
* juntar tabelas;
* criar colunas derivadas;
* filtrar registros ruins;
* converter formatos.

Essa costuma ser a etapa mais cara em tempo e em lógica, porque é onde o dado bruto vira dado útil.

Na AWS, a transformação pode acontecer em **AWS Glue**, **Amazon EMR**, **Athena** ou **Redshift**, dependendo da arquitetura.

---

## Load

Depois do tratamento, o dado é carregado no destino.

Esse destino pode ser:

* um data lake;
* um data warehouse;
* uma tabela curada;
* uma camada pronta para consumo analítico;
* um conjunto de arquivos organizados para consulta.

Na AWS, isso normalmente termina em **S3** ou **Redshift**.

---

## ETL e ELT

Vale separar uma coisa que muita gente mistura.

No **ETL**, você transforma antes de carregar.

No **ELT**, você carrega primeiro e transforma depois, dentro do próprio destino.

O ETL costuma fazer mais sentido quando você quer controlar bem o tratamento antes da carga final.
O ELT costuma aparecer quando o destino tem força suficiente para transformar depois, como acontece em muitas arquiteturas analíticas modernas.

---

## Quando usar

ETL faz sentido quando:

* a origem vem despadronizada;
* existe regra de negócio clara;
* o destino precisa ser confiável;
* você quer chegar em dados mais organizados antes do consumo;
* a qualidade do dado é importante logo na entrada.

---

## Resumo rápido

* **Extract**: pega o dado.
* **Transform**: trata o dado.
* **Load**: grava o dado.
* **ETL**: transforma antes de carregar.
* **ELT**: carrega antes de transformar.

Na AWS, isso aparece muito com **Glue**, **S3**, **Redshift**, **Athena** e **EMR**.
