---
title: Técnicas de Amostragem
layout: default
description: Noções básicas de amostragem para engenharia de dados e DEA
---

# Técnicas de Amostragem

Amostragem é pegar uma parte dos dados para analisar sem precisar olhar a base inteira.

Isso é útil porque, em dados grandes, muitas vezes você só quer validar uma ideia, testar uma regra ou entender a distribuição antes de gastar tempo e recurso com tudo.

---

## Por que isso existe

Você não amostra por charme.

Você amostra porque:

* a base é grande demais;
* o processamento é caro;
* a validação completa demoraria muito;
* você quer explorar os dados primeiro;
* você precisa de uma visão representativa.

---

## Amostragem aleatória

É o tipo mais simples.

Cada linha tem chance parecida de entrar na amostra. Isso ajuda a evitar viés quando você quer uma visão geral.

Exemplo mental: pegar 1% de uma tabela para testar um pipeline.

### Fluxo

<div class="mermaid">
flowchart LR
    A[Base inteira] --> B[Sortear aleatoriamente]
    B --> C[Amostra]
    C --> D[Análise rápida]
</div>

---

## Amostragem estratificada

Aqui você separa por grupo antes de sortear.

Isso é importante quando os grupos têm pesos diferentes e você quer preservar a proporção.

Exemplos:

* pedidos por região;
* clientes por faixa;
* transações por tipo;
* alunos por turma.

Use quando o equilíbrio entre categorias importa. Se você puxar amostra sem pensar, pode acabar com um recorte que parece certo, mas não representa a base.

### Fluxo

<div class="mermaid">
flowchart LR
    A[Base inteira] --> B[Separar por grupos]
    B --> C[Sorteio por grupo]
    C --> D[Amostra proporcional]
</div>

---

## Amostragem sistemática

Aqui você escolhe itens em intervalos fixos.

Exemplo: uma linha a cada 100.

É simples e rápido, mas precisa de cuidado. Se a ordenação da base tiver algum padrão escondido, a amostra pode ficar enviesada.

---

## Quando usar

Use amostragem quando:

* a base é grande demais para testar inteira;
* você quer acelerar uma validação;
* precisa explorar os dados antes de processar em escala;
* o custo e o tempo importam;
* você quer olhar uma parte representativa da base.

---

## O que vale lembrar

* **Aleatória**: sorteio simples.
* **Estratificada**: mantém proporções dos grupos.
* **Sistemática**: pega itens em intervalos.

O ponto mais importante não é decorar o nome. É saber quando a amostra representa bem a realidade e quando ela pode distorcer a leitura.
