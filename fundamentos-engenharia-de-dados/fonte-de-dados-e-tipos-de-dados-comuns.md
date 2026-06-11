---
title: Fonte de Dados e Tipos de Dados Comuns
layout: default
description: Fontes comuns como JDBC e ODBC, e formatos como CSV, JSON, Parquet e Avro
---

# Fonte de Dados e Tipos de Dados Comuns

Esse assunto aparece muito em prova porque é a base de quase todo pipeline.

Antes de pensar em transformação ou modelagem, você precisa saber de onde o dado vem e em que formato ele chega.

---

## Fontes de dados

### JDBC

**JDBC** é uma forma comum de conectar aplicações Java a bancos de dados relacionais.

Na prática, ele aparece muito quando você precisa extrair dados de sistemas como:

* PostgreSQL;
* MySQL;
* SQL Server;
* Oracle;
* Amazon RDS.

Na AWS, o JDBC é muito lembrado quando o **AWS Glue** ou o **Amazon EMR** vão buscar dados em bancos relacionais.

### ODBC

**ODBC** é outra forma de conexão com bancos e fontes tabulares.

Ele é parecido com JDBC na ideia geral: conectar um consumidor a uma fonte de dados relacional. A diferença principal é mais histórica e de ecossistema.

Em prova, o mais importante é entender que tanto JDBC quanto ODBC são formas de acessar dados de bancos e sistemas estruturados.

---

## Formatos comuns

### CSV

É um formato simples e muito usado.

* fácil de gerar;
* fácil de ler;
* comum em trocas entre sistemas;
* geralmente vem com estrutura tabular.

Na AWS, aparece bastante em **S3** e em cargas simples de **Glue** ou **Athena**.

### JSON

É muito comum em APIs, eventos e logs.

* flexível;
* suporta estruturas aninhadas;
* muito usado em dados semiestruturados.

É um formato clássico para ingestão em **S3**, **Athena** e pipelines com **Glue**.

### Parquet

É um formato colunar.

Ele costuma ser melhor para análise porque lê só as colunas necessárias.

Em geral, o Parquet é uma escolha muito boa quando você quer:

* consulta mais eficiente;
* menor custo de leitura;
* melhor uso em analytics.

Na AWS, ele é muito usado em **data lake** e **lakehouse**.

### Avro

É um formato bem comum em integração e streaming.

Ele suporta schema e costuma ser útil quando você quer trocar dados com mais controle sobre estrutura.

Na prática, ele aparece bastante em pipelines com eventos e integrações mais técnicas.

---

## Resumo rápido

* **JDBC / ODBC**: conexão com fontes relacionais.
* **CSV**: simples e tabular.
* **JSON**: flexível e semiestruturado.
* **Parquet**: colunar e eficiente para análise.
* **Avro**: útil em troca de dados com schema.

Se a prova falar de ingestão, extração ou formatos, pense primeiro nisso:

* origem relacional tende a lembrar JDBC/ODBC;
* dado mais livre tende a lembrar JSON;
* analytics em escala tende a lembrar Parquet;
* integração e eventos podem lembrar Avro.
