---

title: Revisão SQL
layout: default
description: Revisão objetiva de SQL para leitura de consultas e cenários comuns da DEA-C01
---
# Revisão SQL

## Visão Geral

A DEA-C01 não é uma prova de SQL, mas SQL aparece bastante em cenários com `Athena`, `Redshift`, validações de pipeline e leitura de dados no `S3`.

O objetivo aqui não é decorar tudo. É conseguir olhar para uma consulta e entender o que ela faz.

---

## Ordem lógica básica

A consulta é escrita em uma ordem, mas a lógica costuma ser entendida assim:

```text
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY
```

Isso ajuda a lembrar:

* `WHERE` filtra linhas antes do agrupamento;
* `HAVING` filtra grupos depois do agrupamento;
* `ORDER BY` só ordena o resultado final.

---

## WHERE

`WHERE` filtra linhas.

```sql
SELECT *
FROM pedidos
WHERE status = 'ENTREGUE';
```

Aqui, só entram pedidos com status `ENTREGUE`.

---

## Agregações

Agregações resumem dados.

Funções comuns:

* `COUNT`;
* `SUM`;
* `AVG`;
* `MIN`;
* `MAX`.

```sql
SELECT SUM(valor_total) AS receita_total
FROM pedidos;
```

---

## GROUP BY

`GROUP BY` agrega por grupo.

```sql
SELECT regiao, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY regiao;
```

Sem `GROUP BY`, você resume tudo junto.
Com `GROUP BY`, você resume por categoria.

Regra importante: coluna no `SELECT` precisa estar no `GROUP BY` ou dentro de uma agregação.

---

## HAVING

`HAVING` filtra grupos depois da agregação.

```sql
SELECT cliente_id, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY cliente_id
HAVING COUNT(*) > 10;
```

Use `WHERE` para linhas.
Use `HAVING` para grupos.

---

## ORDER BY

`ORDER BY` ordena o resultado.

```sql
SELECT cliente_id, SUM(valor_total) AS receita
FROM pedidos
GROUP BY cliente_id
ORDER BY receita DESC;
```

Ele não altera os dados, só a exibição final.

---

## JOIN

`JOIN` junta tabelas.

```sql
SELECT p.id_pedido, c.nome
FROM pedidos p
LEFT JOIN clientes c
    ON p.cliente_id = c.cliente_id;
```

Principais tipos:

| JOIN              | O que faz                             |
| ----------------- | ------------------------------------- |
| `INNER JOIN`      | Mantém só o que existe dos dois lados |
| `LEFT JOIN`       | Mantém tudo da tabela da esquerda     |
| `RIGHT JOIN`      | Mantém tudo da tabela da direita      |
| `FULL OUTER JOIN` | Mantém tudo dos dois lados            |

O `LEFT JOIN` é muito importante porque preserva linhas da tabela principal, mesmo sem correspondência na outra.

---

## Cuidado com JOIN

`JOIN` pode multiplicar linhas.

Se a chave aparece várias vezes nas duas tabelas, o resultado pode crescer sem você perceber.

Exemplo: dois pedidos para o mesmo cliente e dois segmentos para esse cliente podem virar quatro linhas depois do join.

Antes de confiar no resultado, pergunte:

> A chave do join é única em algum dos lados?

---

## DISTINCT

`DISTINCT` remove duplicidades do resultado.

```sql
SELECT DISTINCT cliente_id
FROM pedidos;
```

Mas cuidado: às vezes ele só esconde um `JOIN` mal feito.

---

## CASE WHEN

`CASE WHEN` cria regras condicionais.

```sql
SELECT
    id_pedido,
    CASE
        WHEN valor_total >= 1000 THEN 'ALTO'
        ELSE 'NORMAL'
    END AS faixa_valor
FROM pedidos;
```

É útil para flags, categorias e regras simples.

---

## Pivoting

Pivoting é transformar linhas em colunas.

Exemplo conceitual:

```text
Antes: cliente, mes, valor
Depois: cliente, jan, fev, mar
```

Para a DEA-C01, basta entender a ideia. Cada engine implementa de um jeito.

---

## Como aparece na AWS

SQL aparece principalmente em:

* `Amazon Athena`;
* `Amazon Redshift`;
* `Redshift Spectrum`;
* validações em pipelines;
* consultas rápidas em dados no `S3`.

Mesmo em questões de arquitetura, entender SQL ajuda a interpretar o que está sendo feito com os dados.

---

## Atenção para a prova

* `WHERE` filtra antes do agrupamento.
* `HAVING` filtra depois do agrupamento.
* `GROUP BY` anda junto com agregações.
* `LEFT JOIN` preserva a tabela da esquerda.
* `JOIN` pode multiplicar linhas.
* `DISTINCT` pode esconder problema de join.
* `ORDER BY` só organiza o resultado final.

---

## Resumo rápido

* `WHERE` filtra linhas.
* `HAVING` filtra grupos.
* Agregações resumem.
* `GROUP BY` agrupa.
* `ORDER BY` ordena.
* `JOIN` junta tabelas.
* `DISTINCT` remove duplicados.
* `CASE WHEN` cria regras.

---
