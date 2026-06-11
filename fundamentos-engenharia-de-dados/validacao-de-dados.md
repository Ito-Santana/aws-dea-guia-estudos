---
title: Validação de Dados
layout: default
description: Conceitos básicos de validação de dados em pipelines e contexto AWS
---

# Validação de Dados

Validação de dados é checar se o dado faz sentido antes de ele seguir no pipeline.

Parece simples, mas isso evita muito problema. Se um dado ruim entra no começo, ele pode contaminar relatórios, métricas, análises e até decisões de negócio.

---

## O que se valida

As checagens mais comuns são:

* tipo de dado;
* campo nulo;
* duplicidade;
* formato;
* faixa válida;
* chave obrigatória;
* consistência entre colunas.

Exemplos simples:

* data precisa estar no formato esperado;
* preço não pode ser negativo;
* identificador único não pode repetir;
* status precisa bater com a regra do domínio.

---

## Quando validar

A validação pode acontecer em vários pontos:

* na ingestão;
* depois da transformação;
* antes da carga final;
* antes de publicar a tabela para consumo.

Na prática, isso evita que dados errados avancem demais no pipeline.

---

## Por que isso importa

Se os dados estão errados, o problema não fica só na origem.

Ele aparece depois como:

* relatório errado;
* métrica errada;
* retrabalho;
* quebra de pipeline;
* custo desnecessário;
* decisão ruim.

---

## Validação e qualidade

Validação é parte da qualidade de dados, mas não cobre tudo.

Qualidade também envolve:

* completude;
* precisão;
* consistência;
* atualidade;
* unicidade;
* confiabilidade.

Ou seja: validar é impedir que o erro siga adiante. Qualidade é um pouco mais ampla que isso.

---

## Resumo rápido

Validação de dados é a checagem que impede dado ruim de continuar no fluxo.

Se o dado não bate com as regras mínimas, ele precisa ser tratado antes de chegar no consumo final.
