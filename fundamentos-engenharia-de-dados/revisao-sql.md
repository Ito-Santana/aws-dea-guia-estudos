---
title: Revisao SQL
layout: default
description: Revisao objetiva de SQL para leitura de consultas e cenarios comuns da DEA-C01
---

# Revisão SQL

## Visão Geral

A DEA-C01 não é prova de SQL, mas ela assume que você não se perde quando aparece uma consulta, um `JOIN`, um `GROUP BY` ou um filtro um pouco mais chatinho.

Se SQL ainda está inseguro, vale revisar agora. Senão, o resto do conteúdo começa a parecer mais difícil do que realmente é.

## O que mais vale revisar

Para esse contexto de prova, eu focaria em:

- `WHERE`;
- agregações;
- `GROUP BY`;
- `ORDER BY`;
- `JOIN`;
- noção de pivoting.

Não precisa transformar isso em curso completo de banco de dados. A ideia é conseguir ler consulta e entender o efeito dela.

## Filtrar com WHERE

`WHERE` é o filtro.

É ele que corta o universo antes de qualquer agrupamento ou ordenação.

Exemplo:

```sql
SELECT *
FROM pedidos
WHERE status = 'ENTREGUE';
```

Esse tipo de coisa aparece o tempo todo em questões de leitura de consulta.

## Agregações

Agregação é quando você deixa de olhar linha por linha e passa a resumir.

Funções mais comuns:

- `COUNT`
- `SUM`
- `AVG`
- `MIN`
- `MAX`

Exemplo:

```sql
SELECT SUM(valor_total) AS receita_total
FROM pedidos;
```

## GROUP BY

O `GROUP BY` entra quando você quer resumir por grupo.

Exemplo:

```sql
SELECT regiao, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY regiao;
```

Sem `GROUP BY`, você resume tudo junto. Com `GROUP BY`, você resume por categoria.

Essa é uma daquelas coisas que parecem triviais, mas muita gente trava quando a consulta mistura agregação com mais de uma coluna.

## ORDER BY

`ORDER BY` só organiza o resultado final.

Exemplo:

```sql
SELECT cliente_id, receita
FROM vendas
ORDER BY receita DESC;
```

Bom para ranking, relatório e leitura de resultado.

## JOIN

Aqui normalmente mora a parte mais importante.

`JOIN` junta tabelas. Se isso não estiver claro, boa parte das questões com SQL fica confusa.

### INNER JOIN

Traz só o que existe dos dois lados.

### LEFT JOIN

Traz tudo da tabela da esquerda, mesmo quando não há correspondência na direita.

Esse costuma ser o join mais importante para leitura de cenários, porque muita questão quer saber se linhas serão preservadas ou perdidas.

### RIGHT JOIN

É o espelho do `LEFT JOIN`. Aparece menos no dia a dia.

### FULL OUTER JOIN

Traz tudo de ambos os lados, casando o que der e mantendo o que sobrar.

Exemplo:

```sql
SELECT p.id_pedido, c.nome
FROM pedidos p
LEFT JOIN clientes c
    ON p.id_cliente = c.id_cliente;
```

## Pivoting

Pivoting é mais conceito do que comando específico, porque cada engine implementa isso de um jeito.

A ideia é transformar linhas em colunas.

Exemplo mental:

- antes: uma linha para cada mês;
- depois: uma coluna para cada mês.

Isso aparece mais em relatório e reorganização de resultado.

## Como isso aparece na AWS

Você vai encontrar SQL ou SQL-like em vários pontos:

- `Amazon Athena`;
- `Amazon Redshift`;
- transformações e validações em pipelines;
- consultas para inspeção rápida em dados no `S3`.

Mesmo quando a prova está falando de arquitetura, entender o básico de SQL ajuda a interpretar o que a questão quer fazer com os dados.

## Pegadinhas para a prova

- `WHERE` filtra antes do agrupamento.
- `GROUP BY` e agregação andam juntos.
- `LEFT JOIN` preserva a tabela da esquerda.
- consulta errada em `JOIN` pode multiplicar linhas sem você perceber.
- às vezes a questão não quer que você escreva SQL; ela quer só que você entenda o resultado lógico da consulta.

## Quando usar

SQL entra praticamente o tempo todo em engenharia de dados para:

- explorar;
- validar;
- agregar;
- juntar tabelas;
- preparar consumo analítico.

## Quando não usar

Não force SQL como se ele resolvesse tudo. Em alguns cenários, o desafio está mais em ingestão, particionamento, streaming ou processamento distribuído do que na consulta em si.

## Resumo rápido

- `WHERE` filtra.
- agregação resume.
- `GROUP BY` cria grupos para resumir.
- `ORDER BY` ordena.
- `JOIN` junta tabelas.

## Checklist para prova

- [ ] Conseguir ler `GROUP BY` sem hesitar
- [ ] Entender diferença entre `INNER JOIN` e `LEFT JOIN`
- [ ] Reconhecer o efeito de `ORDER BY`
- [ ] Lembrar das agregações básicas
- [ ] Saber que `Athena` e `Redshift` usam muito esse repertório
