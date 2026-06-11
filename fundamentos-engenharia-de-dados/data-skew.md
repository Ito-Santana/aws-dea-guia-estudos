---
title: Data Skew
layout: default
description: Conceito básico de data skew e impacto em processamento distribuído
---

# Data Skew

**Data skew** acontece quando a distribuição dos dados fica desigual.

Na prática, isso quer dizer que algumas chaves, partições ou grupos recebem muito mais dados que os outros. Em processamento distribuído, isso costuma criar gargalo.

---

## Exemplo simples

Imagine um job que distribui registros por `cliente_id`.

Se um cliente concentra muitos milhões de registros e os outros têm bem menos, uma partição vai ficar muito mais pesada que as outras.

Resultado:

* um executor trabalha demais;
* outros ficam ociosos;
* o job fica mais lento;
* pode até falhar por falta de memória.

---

## Onde isso aparece

Data skew aparece bastante em:

* Spark;
* Glue;
* joins grandes;
* agregações por chave;
* partições ruins em data lake.

Na AWS, isso é muito relevante quando você usa **AWS Glue** ou **Amazon EMR**.

---

## Como perceber

Alguns sinais comuns:

* um job demora muito mais que o esperado;
* uma etapa específica fica travada;
* o uso de recursos fica desigual;
* joins ou group by começam a sofrer.

---

## Como lidar

As soluções mais comuns são:

* mudar a chave de partição;
* distribuir melhor os dados;
* usar broadcast join quando fizer sentido;
* tratar valores muito concentrados;
* revisar o desenho das partições.

---

## Resumo rápido

Data skew é desequilíbrio na distribuição dos dados.

Em prova, pense assim:

* poucos dados em uma parte e muitos em outra = problema de distribuição;
* isso atrapalha processamento paralelo;
* Glue e EMR são contextos típicos para lembrar desse tema.
