---
title: Fonte de Dados e Tipos de Dados Comuns
layout: default
description: Fontes comuns como JDBC e ODBC, e formatos como CSV, JSON, Parquet, Avro e XML
---

# Fonte de Dados e Tipos de Dados Comuns

Antes de pensar em transformação, modelagem ou analytics, vale entender duas coisas: de onde o dado vem e em que formato ele chega.

Esse assunto aparece muito porque quase todo pipeline de dados começa por aqui.

---

## Fontes de dados

### JDBC

**JDBC** é uma API de Java para acessar dados tabulares, principalmente bancos relacionais.

Na prática, você usa JDBC quando a aplicação que está lendo ou escrevendo dado é Java ou roda no ecossistema Java. É muito comum em integrações com:

* PostgreSQL;
* MySQL;
* SQL Server;
* Oracle;
* Amazon RDS;
* outras fontes relacionais.

O ponto principal aqui é: JDBC fala a linguagem do Java.

### ODBC

**ODBC** é uma API mais genérica para acesso a banco de dados.

Ela não nasceu presa a uma linguagem específica. A ideia é ser uma camada de acesso que conversa com drivers diferentes em tempo de execução. O ODBC ficou muito associado ao mundo Windows porque nasceu no ecossistema Microsoft e historicamente aparece muito em ferramentas de desktop, relatórios e integração com DSN, mas ele não é exclusivo do Windows.

Hoje você encontra ODBC também em outras plataformas, dependendo do driver e do gerenciador instalado.

O jeito mais simples de pensar é:

* **JDBC**: mais natural em aplicações Java;
* **ODBC**: mais genérico, muito comum em ferramentas e integrações variadas.

### Diferença prática entre JDBC e ODBC

Se você quiser uma regra simples para prova e estudo:

* se o consumidor é Java, pense em **JDBC**;
* se a ideia é uma camada mais universal de acesso a banco, pense em **ODBC**;
* os dois normalmente aparecem com fontes relacionais e dados tabulares.

Na AWS, isso aparece bastante quando Glue, Spark, EMR ou alguma ferramenta de integração precisa buscar dado em banco relacional.

---

## Tipos de dados comuns

### CSV

O **CSV** é o formato mais direto de todos.

Ele é bom quando o dado é tabular e você quer algo simples de gerar, ler e trocar entre sistemas.

Use CSV quando:

* o arquivo é basicamente uma tabela;
* a estrutura é simples;
* você quer facilidade de interoperar com outras ferramentas;
* não precisa de nested data.

Ponto fraco: ele não lida bem com estrutura complexa, tipos ricos ou volume grande com eficiência.

### JSON

O **JSON** é muito usado em APIs, eventos e logs.

Ele funciona bem quando o dado vem com estrutura flexível, campos opcionais ou objetos aninhados.

Use JSON quando:

* a origem é API;
* o dado tem estrutura variável;
* você quer algo legível e fácil de integrar;
* os registros podem ter campos diferentes entre si.

JSON é uma escolha muito natural para ingestão, mas não costuma ser a melhor opção para analytics pesado em larga escala.

### Parquet

O **Parquet** é um formato colunar.

Isso faz diferença porque, em análise, normalmente você não quer ler a linha inteira. Você quer ler só as colunas que importam naquela consulta.

Use Parquet quando:

* o foco é consulta analítica;
* a base é grande;
* você quer economizar leitura e custo;
* os dados vão ficar em data lake;
* a maior parte do consumo é leitura e agregação.

Entre os formatos dessa lista, o Parquet costuma ser a melhor escolha para análise em S3.

### Avro

O **Avro** é muito usado para serialização e integração entre sistemas.

Ele é bom quando você quer transportar dados com schema e manter melhor controle sobre evolução de estrutura.

Use Avro quando:

* o dado vai trafegar entre sistemas;
* você está lidando com streaming ou mensageria;
* schema evolution importa;
* a prioridade é serialização compacta e leitura mais ligada ao registro inteiro do que a colunas soltas.

Se eu resumir sem rodeio:

* **Parquet** é melhor para leitura analítica;
* **Avro** é melhor para troca de dados e pipelines com schema.

### XML

O **XML** é mais verboso e mais antigo, mas ainda aparece bastante em integrações legadas e sistemas corporativos.

Use XML quando:

* a fonte já usa XML por padrão;
* você está lidando com integração corporativa antiga;
* a estrutura vem por tags e hierarquia;
* você precisa interoperar com sistemas que já falam XML.

Para análise moderna, XML normalmente não é a primeira escolha. Ele aparece mais por compatibilidade do que por eficiência.

---

## Como escolher sem complicar

Se eu fosse simplificar a escolha:

* **JDBC**: acesso Java a banco relacional;
* **ODBC**: acesso mais genérico a banco, muito comum em integrações e ferramentas;
* **CSV**: tabela simples;
* **JSON**: dado flexível e semiestruturado;
* **Parquet**: analytics em escala;
* **Avro**: integração e schema evolution;
* **XML**: legado e integrações corporativas.

---

## Resumo rápido

* JDBC e ODBC são formas de acessar dados em bancos.
* JDBC é mais natural no mundo Java.
* ODBC é mais genérico e historicamente muito associado ao ecossistema Microsoft, mas não fica preso ao Windows.
* CSV serve para tabela simples.
* JSON serve para dado flexível.
* Parquet serve para leitura analítica.
* Avro serve muito bem para troca de dados e streaming.
* XML aparece muito em integrações antigas.
