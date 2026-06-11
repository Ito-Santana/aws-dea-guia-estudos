---
title: Validação de Dados
layout: default
description: Conceitos básicos de validação de dados em pipelines e contexto AWS
---

# Validação de Dados

Validação de dados é checar se o dado está certo antes de deixar ele seguir no pipeline.

Isso parece simples, mas é uma das partes mais importantes de engenharia de dados. Se você não valida, o erro entra no início e aparece lá na frente em BI, relatório ou modelo analítico.

---

## O que costuma ser validado

Algumas checagens básicas:

* tipo de dado;
* valor nulo;
* duplicidade;
* faixa válida;
* formato esperado;
* chave obrigatória;
* consistência entre colunas.

Exemplo:

* data não pode vir no formato errado;
* preço não pode ser negativo;
* `id` não pode repetir quando deveria ser único.

---

## Quando validar

A validação pode acontecer:

* na ingestão;
* antes da carga final;
* depois da transformação;
* antes de publicar uma tabela curada.

Na AWS, isso aparece bastante em pipelines com **Glue**, **Athena**, **EMR** e também em soluções com **Lake Formation** e **Redshift**.

---

## Por que isso importa

Se os dados estão ruins, o problema não fica só na origem.

Ele vira:

* relatório errado;
* decisão errada;
* retrabalho;
* custo extra;
* quebra de pipeline.

---

## Validação e qualidade

Validação é parte da qualidade de dados, mas não é tudo.

Qualidade também envolve:

* completude;
* precisão;
* consistência;
* atualidade;
* unicidade.

---

## Resumo rápido

Validação de dados é a checagem que impede dado ruim de seguir adiante.

Na prova da AWS, pense nela como uma proteção básica do pipeline.
Se o dado não passa nas regras mínimas, ele não deve chegar na camada de consumo.
