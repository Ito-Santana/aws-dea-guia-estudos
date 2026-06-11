---
title: Revisão SQL
layout: default
description: Revisão prática de SQL para fundamentos de engenharia de dados e DEA
---

# Revisão SQL

SQL é uma parte que a DEA não vai ensinar do zero. A ideia é que você já consiga ler consulta, entender o que ela faz e montar as bases mais comuns sem travar.

Se essa parte ainda está fraca, vale estudar com calma ou fazer um curso básico antes de avançar. Não é vergonha nenhuma; só evita ficar tropeçando no resto do conteúdo.

---

## O que o SQL mais cobra

Na prática, quase tudo gira em torno de quatro blocos:

* filtrar;
* agrupar;
* ordenar;
* combinar tabelas.

Se você entende bem isso, já cobre uma boa parte do que aparece na revisão.

---

## Agregação

Agregação é quando você resume os dados.

Em vez de olhar linha por linha, você quer responder perguntas como:

* quantos pedidos existem;
* quanto foi vendido no total;
* qual é a média;
* qual foi o maior valor;
* qual foi o menor valor.

Funções mais comuns:

* `COUNT`
* `SUM`
* `AVG`
* `MIN`
* `MAX`

Exemplo:

```sql
SELECT COUNT(*) AS total_pedidos
FROM pedidos;
```

---

## GROUP BY

`GROUP BY` serve para separar os dados em grupos antes de agregar.

Se você quer o total por região, por mês ou por cliente, é aqui que entra.

Exemplo:

```sql
SELECT regiao, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY regiao;
```

Se quiser o total por região e por status ao mesmo tempo, também dá.

```sql
SELECT regiao, status, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY regiao, status;
```

### Fluxo mental

<div class="mermaid">
flowchart LR
    A[Linhas soltas] --> B[GROUP BY]
    B --> C[Grupos]
    C --> D[Agregação]
    D --> E[Resultado resumido]
</div>

---

## ORDER BY

`ORDER BY` serve para ordenar o resultado final.

Você pode ordenar:

* crescente;
* decrescente;
* por mais de uma coluna.

Exemplo:

```sql
SELECT nome, receita
FROM vendas
ORDER BY receita DESC;
```

Isso aparece muito em ranking, relatório e consulta analítica.

---

## JOIN

`JOIN` é o que combina tabelas.

Esse é um dos assuntos mais importantes de SQL. Se você não entende join, o resto fica capenga.

### INNER JOIN

Traz só os registros que existem nas duas tabelas.

Use quando você só quer o que realmente casou.

### LEFT JOIN

Traz tudo da tabela da esquerda e o que casar da direita.

Use quando a tabela principal não pode perder linhas.

### RIGHT JOIN

É o espelho do `LEFT JOIN`, mas aparece menos no dia a dia.

### FULL OUTER JOIN

Traz tudo dos dois lados.

Use quando você quer enxergar tanto o que casou quanto o que ficou de fora.

### CROSS JOIN

Gera todas as combinações possíveis.

É menos comum, mas em alguns casos faz sentido.

### Visão rápida

<div class="mermaid">
flowchart TB
    A[Tabela A] --> I[INNER JOIN]
    B[Tabela B] --> I

    A --> L[LEFT JOIN]
    B --> L

    A --> F[FULL OUTER JOIN]
    B --> F
</div>

---

## Pivoting

Pivoting é quando você transforma linhas em colunas.

Isso não aparece em todo banco da mesma forma, mas o conceito é importante.

Exemplo mental:

* antes: uma linha para cada mês;
* depois: uma coluna para cada mês.

É uma reorganização que ajuda muito em relatório e visualização.

---

## O que vale guardar

Se a questão falar de SQL, normalmente ela está testando se você sabe:

* resumir dados com agregação;
* separar grupos com `GROUP BY`;
* ordenar com `ORDER BY`;
* combinar tabelas com `JOIN`;
* reorganizar dados com pivoting.

---

## Resumo rápido

* **Agregação**: resume dados.
* **GROUP BY**: cria grupos.
* **ORDER BY**: organiza o resultado.
* **JOIN**: junta tabelas.
* **Pivoting**: muda linhas em colunas.

Se SQL ainda não está natural, vale revisar antes de seguir. Isso evita sofrimento desnecessário no resto do estudo.
