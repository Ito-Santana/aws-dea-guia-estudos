---
title: Data Skew
layout: default
description: Conceito básico de data skew e impacto em processamento distribuído
---

# Data Skew

**Data skew** é quando os dados ficam distribuídos de forma desigual.

Em vez de todas as partições, chaves ou grupos receberem volumes parecidos, um lado fica muito mais pesado que os outros. Em processamento distribuído, isso vira gargalo.

---

## O que acontece

Imagine um job que distribui registros por `cliente_id`.

Se um único cliente concentra uma quantidade enorme de registros, essa partição fica sobrecarregada.

Enquanto isso:

* uma parte do cluster trabalha demais;
* outras partes ficam ociosas;
* o job demora mais;
* o consumo de memória sobe;
* o processamento pode até falhar.

---

## Onde isso aparece

Data skew aparece muito em:

* Spark;
* Glue;
* joins grandes;
* agregações;
* partições mal desenhadas.

Na prática, é um problema de distribuição. O código pode estar certo e ainda assim o job ficar ruim porque os dados não estão equilibrados.

---

## Como perceber

Alguns sinais comuns:

* uma etapa demora muito mais que as outras;
* um executor fica muito mais carregado que os demais;
* o uso de CPU e memória fica desigual;
* joins e group by ficam mais lentos que o esperado;
* o job parece “preso” em uma parte específica.

---

## Como lidar

As saídas mais comuns são:

* mudar a chave de particionamento;
* distribuir melhor os dados;
* tratar valores muito concentrados;
* usar broadcast join quando fizer sentido;
* revisar a forma de agrupar ou ordenar os dados.

Nem sempre existe uma solução única. Às vezes o problema está na modelagem; às vezes está na chave de junção; às vezes está na forma como a base foi particionada.

---

## Resumo rápido

Data skew é desequilíbrio na distribuição dos dados.

Se uma parte do processamento recebe muito mais volume que as outras, o paralelo deixa de funcionar bem.

Em prova, pense nisso como um problema de concentração de dados que atrapalha performance.
