---

title: Técnicas de Amostragem
layout: default
description: Técnicas de amostragem para exploração, validação e análise de dados
---

# Técnicas de Amostragem

## Visão Geral

Amostragem é trabalhar com uma parte dos dados em vez de processar a base inteira.
A ideia é usar um recorte menor para investigar, testar ou validar alguma coisa antes de gastar mais tempo e processamento.

---

## Por que isso importa?

Às vezes você só quer responder perguntas iniciais, como:

* os campos estão vindo preenchidos?
* o timestamp está em qual formato?
* existem valores fora do padrão?
* a regra de transformação parece funcionar?
* a distribuição dos dados faz sentido?

Nesses casos, uma boa amostra ajuda a ganhar velocidade.

Mas tem um cuidado importante: **amostra não é garantia de verdade absoluta**. Ela ajuda a entender o dado, mas pode esconder casos raros, outliers ou grupos pequenos.

---

## Amostragem aleatória

A amostragem aleatória escolhe registros ao acaso.

É útil quando você quer uma visão geral da base, sem favorecer uma ordem ou grupo específico.

Exemplo:

```text
De 10 milhões de eventos, selecionar 100 mil aleatoriamente para análise inicial.
```

Ela funciona bem para exploração rápida, mas pode falhar se a base for muito desbalanceada.

Imagine uma base em que 99% dos registros são de clientes comuns e 1% são de clientes enterprise. Uma amostra aleatória pequena pode quase não trazer clientes enterprise, mesmo eles sendo importantes para a análise.

---

## Amostragem estratificada

A amostragem estratificada separa os dados em grupos antes de selecionar a amostra.

Esses grupos são chamados de estratos.

Exemplo:

```text
Separar clientes por plano:
- Free
- Pro
- Enterprise

Depois, tirar uma amostra de cada grupo.
```

Ela é útil quando você precisa garantir que grupos importantes apareçam na análise.

Em dados reais, isso faz bastante sentido. Às vezes um grupo é pequeno em volume, mas muito importante para o negócio.

Exemplos de estratos:

* região;
* plano do cliente;
* tipo de transação;
* canal de venda;
* categoria de produto;
* status do pedido.

Se a base é desbalanceada, a estratificada costuma ser melhor que uma amostra aleatória simples.

---

## Amostragem sistemática

A amostragem sistemática escolhe dados em intervalos fixos.

Exemplo:

```text
Pegar 1 registro a cada 100.
```

Ou:

```text
Analisar 1 arquivo a cada lote recebido.
```

Ela é simples de implementar e pode ser útil em validações rápidas.

O cuidado é que a ordem dos dados pode ter algum padrão escondido.

Por exemplo: se os dados estão ordenados por horário e você sempre pega o mesmo intervalo, talvez acabe olhando sempre eventos parecidos. Nesse caso, a amostra pode ficar enviesada.

---

## Exemplo prático na AWS

Imagine uma empresa com bilhões de eventos armazenados no `Amazon S3`.

Antes de converter tudo para `Parquet`, o time quer entender melhor os dados.

Eles podem pegar uma amostra para validar:

* campos nulos;
* tipos de evento;
* formato de timestamp;
* valores fora do padrão;
* distribuição por cliente ou região.

Depois dessa análise inicial, o pipeline fica mais seguro para processar a base completa.

```mermaid
flowchart LR
    A[Base completa no S3] --> B[Amostra inicial]
    B --> C[Analise exploratoria]
    C --> D[Ajuste do pipeline]
    D --> E[Processamento completo]
```

---

## Pegadinhas para a prova

* Amostra rápida não significa amostra representativa.
* Amostragem aleatória pode perder grupos pequenos.
* Amostragem estratificada ajuda quando existem grupos importantes.
* Amostragem sistemática pode gerar viés se houver padrão na ordenação.
* Nem toda validação pode ser feita só com amostra.
* Para casos raros ou críticos, pode ser necessário analisar a base completa.

---

## Quando usar

Use amostragem quando você quer:

* explorar uma base nova;
* testar uma transformação;
* validar schema;
* investigar qualidade;
* reduzir custo em análise inicial;
* entender distribuição antes do processamento completo.

---


## Comparação rápida

| Técnica       | Ideia                         | Cuidado                         |
| ------------- | ----------------------------- | ------------------------------- |
| Aleatória     | Seleciona registros ao acaso  | Pode perder grupos pequenos     |
| Estratificada | Amostra por grupos            | Precisa definir bem os grupos   |
| Sistemática   | Seleciona em intervalos fixos | Pode sofrer viés pela ordenação |

---

## Resumo rápido

Amostragem é usar uma parte dos dados para explorar, testar ou validar antes de processar tudo.

A aleatória é simples.
A estratificada é melhor quando existem grupos importantes.
A sistemática é prática, mas exige cuidado com padrões escondidos.

Em Engenharia de Dados, amostragem ajuda a economizar tempo e custo, principalmente em bases grandes no `S3`, jobs no `Glue` e análises exploratórias.

---
