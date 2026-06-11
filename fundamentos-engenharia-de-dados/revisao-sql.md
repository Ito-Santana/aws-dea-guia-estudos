---
title: Revisão SQL
layout: default
description: Revisão prática de SQL para fundamentos de engenharia de dados e prova AWS
---

# Revisão SQL

A DEA não costuma cobrar SQL do zero. Ela parte do pressuposto de que você já consegue ler, entender e montar consultas básicas.

Então, se SQL ainda não está confortável para você, vale estudar com calma ou fazer um curso na internet antes de seguir. Isso ajuda muito, porque esse conteúdo aparece o tempo todo quando a ideia é trabalhar com dados.

---

## Agregação

Agregação é quando você resume dados.

Em vez de olhar linha por linha, você quer responder coisas como:

* quantos pedidos foram feitos;
* qual foi o total vendido;
* qual a média de consumo;
* qual o maior ou menor valor.

Funções comuns:

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

`GROUP BY` serve para agrupar os dados antes de agregar.

Se você quer o total por cliente, por mês ou por região, ele entra aqui.

Exemplo:

```sql
SELECT regiao, COUNT(*) AS total_pedidos
FROM pedidos
GROUP BY regiao;
```

Se quiser agregar por mais de uma coluna, dá para fazer também.

---

## ORDER BY

`ORDER BY` serve para ordenar o resultado.

Você pode ordenar:

* crescente;
* decrescente;
* por uma ou mais colunas.

Exemplo:

```sql
SELECT nome, receita
FROM vendas
ORDER BY receita DESC;
```

Na prática, isso aparece muito em listas de ranking, relatórios e consultas de análise.

---

## Pivoting

Pivoting é quando você transforma linhas em colunas.

Isso não é uma coisa que aparece em todo banco do mesmo jeito, mas o conceito é importante: você está reorganizando os dados para facilitar leitura ou relatório.

Exemplo mental:

* antes: uma linha por mês;
* depois: uma coluna para cada mês.

Isso pode aparecer em ferramentas de banco, SQL analítico ou transformações antes de publicar uma tabela final.

---

## JOIN types

`JOIN` é o que você usa para combinar tabelas.

Esse é um dos tópicos mais importantes de SQL.

### INNER JOIN

Traz só os registros que existem nas duas tabelas.

Exemplo de uso: pedidos que realmente têm cliente correspondente.

### LEFT JOIN

Traz tudo da tabela da esquerda e o que combinar da direita.

Se não houver correspondência, a parte da direita vem nula.

É muito útil quando você quer manter a base principal inteira.

### RIGHT JOIN

É o inverso do `LEFT JOIN`, mas aparece menos no dia a dia.

### FULL OUTER JOIN

Traz tudo das duas tabelas.

É útil quando você quer enxergar os dados que casam e os que ficaram de fora.

### CROSS JOIN

Gera combinação de todos com todos.

É menos comum, mas pode aparecer em cenários específicos.

---

## O que vale guardar

Se a questão falar de SQL, normalmente ela está testando se você entende:

* como resumir dados com agregação;
* como agrupar com `GROUP BY`;
* como ordenar com `ORDER BY`;
* como reorganizar dados com pivoting;
* como combinar tabelas com diferentes tipos de `JOIN`.

Na prática, a DEA espera que essa base já esteja pronta.

---

## Resumo rápido

* **Agregação**: resume dados.
* **GROUP BY**: separa por grupo antes de agregar.
* **ORDER BY**: ordena o resultado.
* **Pivoting**: transforma linhas em colunas.
* **JOIN**: combina tabelas.

Se SQL ainda estiver fraco, estude isso antes. Faz diferença real no resto da preparação.
