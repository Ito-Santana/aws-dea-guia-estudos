---
title: Técnicas de Amostragem
layout: default
description: Noções básicas de amostragem para engenharia de dados e prova AWS
---

# Técnicas de Amostragem

Amostragem é quando você pega uma parte dos dados para analisar sem precisar olhar a base inteira.

Isso é útil porque nem sempre vale a pena processar tudo logo de cara. Às vezes você quer testar uma hipótese, validar uma regra ou só ter uma noção rápida da distribuição dos dados.

---

## Por que amostrar

As razões mais comuns são:

* a base é grande demais;
* o processamento custa caro;
* o teste completo demoraria muito;
* você quer explorar os dados antes de rodar algo maior;
* você só precisa de uma visão representativa.

---

## Amostragem aleatória

É o tipo mais simples.

Cada linha tem uma chance de entrar na amostra. Isso ajuda quando você quer uma visão geral sem favorecer um grupo específico.

Exemplo mental: pegar 1% dos registros de uma tabela para testar um pipeline.

---

## Amostragem estratificada

Aqui você separa os dados por grupo antes de sortear.

Isso é importante quando os grupos têm peso diferente e você não quer perder essa proporção.

Exemplo:

* pedidos por região;
* clientes por faixa;
* transações por tipo.

Esse tipo é bom quando o equilíbrio entre categorias importa.

---

## Amostragem sistemática

Nesse caso, você pega itens em intervalos fixos.

Exemplo: uma linha a cada 100.

É simples e pode funcionar bem, mas você precisa tomar cuidado para não criar viés se houver algum padrão na ordenação dos dados.

---

## Quando usar

Use amostragem quando:

* a base é grande demais para testar inteira;
* você quer acelerar uma validação;
* precisa explorar os dados antes de processar em escala;
* o custo e o tempo importam;
* você quer checar a qualidade de uma parte representativa.

---

## Resumo rápido

* **Aleatória**: sorteio simples.
* **Estratificada**: preserva proporções dos grupos.
* **Sistemática**: pega itens em intervalos.

O ponto principal não é decorar o nome. É entender quando uma amostra pode representar bem a base e quando ela pode distorcer a leitura.
