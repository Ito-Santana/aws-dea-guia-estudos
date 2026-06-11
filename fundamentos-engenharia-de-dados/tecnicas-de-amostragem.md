---
title: Técnicas de Amostragem
layout: default
description: Noções básicas de amostragem para engenharia de dados e prova AWS
---

# Técnicas de Amostragem

Amostragem é pegar uma parte do conjunto de dados para analisar sem precisar olhar tudo.

Isso é útil quando o volume é grande, o processamento custa caro ou você só quer validar uma hipótese rápida.

---

## Ideia básica

Em vez de trabalhar com a base inteira, você pega uma amostra representativa.

Na AWS, isso pode aparecer em:

* validação de pipeline;
* testes com dados grandes;
* exploração inicial;
* checagem de qualidade;
* jobs em Spark ou Glue.

---

## Tipos comuns

### Amostragem aleatória

Cada linha tem chance de entrar na amostra.

É a forma mais simples e costuma ser a primeira que vem à mente.

### Amostragem estratificada

Você separa por grupos antes de sortear.

Isso é útil quando você não quer perder a proporção entre categorias importantes.

Exemplo:

* clientes por região;
* transações por tipo;
* pedidos por status.

### Amostragem sistemática

Você escolhe itens em um intervalo fixo.

Exemplo: pegar uma linha a cada 100.

---

## Quando usar

Use amostragem quando:

* a base é grande demais para testar tudo;
* você quer acelerar validações;
* precisa explorar dados antes de processar em escala;
* o custo ou o tempo do processamento importam.

---

## Resumo rápido

* **Aleatória**: simples e comum.
* **Estratificada**: mantém proporção dos grupos.
* **Sistemática**: pega itens em intervalos.

Na prova, o foco costuma ser entender por que amostrar e qual tipo ajuda a não distorcer o resultado.
