---
title: Data Skew
layout: default
description: Conceito básico de data skew e impacto em processamento distribuído
---

# Data Skew

**Data skew** é quando os dados ficam distribuídos de forma desigual.

Em vez de cada partição, chave ou grupo receber um volume parecido, uma parte fica muito mais pesada que as outras. Em processamento distribuído, isso costuma virar gargalo.

---

## O que acontece

Imagine um job que distribui os registros por `cliente_id`.

Se um único cliente concentra milhões de linhas, essa partição vai ficar sobrecarregada.

Enquanto isso:

* uma parte do cluster trabalha demais;
* outras ficam paradas;
* o job demora mais;
* a memória sobe;
* o processo pode até falhar.

### Visão simples

<div class="mermaid">
flowchart LR
    A[Dados equilibrados] --> B[Processamento paralelo]
    C[Dados concentrados] --> D[Uma partição pesada]
    D --> E[Lentidão / gargalo]
</div>

---

## Onde isso aparece

Data skew aparece muito em:

* Spark;
* Glue;
* joins grandes;
* agregações;
* partições mal desenhadas.

Na prática, o problema não é só o volume. É a concentração do volume em poucos grupos.

---

## Como perceber

Alguns sinais comuns:

* uma etapa demora muito mais que as outras;
* um executor fica bem mais carregado que os demais;
* CPU e memória ficam desequilibrados;
* joins e group by ficam lentos;
* o job parece travar em uma parte específica.

---

## Como lidar

As saídas mais comuns são:

* mudar a chave de particionamento;
* distribuir melhor os dados;
* tratar valores muito concentrados;
* usar broadcast join quando fizer sentido;
* revisar a forma de agrupar ou ordenar.

Nem sempre existe uma solução única. Às vezes o problema está na modelagem, às vezes na chave, às vezes na forma de particionar.

---

## Resumo rápido

Data skew é desequilíbrio na distribuição dos dados.

Se uma parte do processamento recebe muito mais volume que as outras, o paralelismo deixa de ajudar.

Em prova, pense nisso como um problema de concentração que derruba performance.
