---
title: Data Mesh
layout: default
description: Arquitetura distribuída de dados com foco em domínio, responsabilidade e governança
---

# Data Mesh

O **data mesh** entra na conversa quando o time central de dados já não dá conta de tudo sozinho.

Isso costuma acontecer em empresas maiores, com várias áreas produzindo e consumindo dados ao mesmo tempo. Nessa fase, tentar centralizar tudo em um único time começa a virar fila, atraso e dependência demais. O data mesh propõe outra ideia: cada domínio de negócio assume mais responsabilidade pelos próprios dados.

Em vez de pensar só em “um time de dados”, a empresa passa a pensar em **times donos de domínios**. Vendas cuida de vendas, financeiro cuida de financeiro, logística cuida de logística. Cada área conhece melhor os dados que gera e usa no dia a dia.

Na AWS, isso normalmente aparece junto de S3, Glue, Athena e Lake Formation. A tecnologia ajuda, mas a mudança mesmo é de organização.

---

## A ideia por trás

Se eu tiver que resumir em uma frase, data mesh é isso:

**os dados deixam de ser um problema exclusivo de um time central e passam a ser responsabilidade compartilhada pelos domínios que realmente entendem aquele assunto.**

Isso não significa bagunça. Significa distribuir responsabilidade com regra, padrão e governança.

### Visão simples

<div class="mermaid">
flowchart LR
    A[Domínio Vendas] --> D[Dados de vendas]
    B[Domínio Financeiro] --> E[Dados financeiros]
    C[Domínio Logística] --> F[Dados de logística]

    D --> G[Plataforma de dados]
    E --> G
    F --> G

    G --> H[Consumo analítico]
    G --> I[BI / ML]
</div>

---

## O que muda na prática

Num modelo mais tradicional, o time central de dados recebe pedidos de tudo quanto é lado, modela o dado, cria pipeline, publica tabela e tenta manter isso saudável.

No data mesh, essa responsabilidade fica mais próxima de quem entende o assunto. O time central não some, mas muda de papel. Ele vira mais uma plataforma e menos um gargalo.

O resultado esperado é:

* menos fila para atender solicitações;
* mais autonomia para os domínios;
* dados mais próximos do contexto de negócio;
* menos dependência de uma equipe única para tudo.

---

## O que precisa existir

Para isso funcionar, algumas coisas precisam estar no lugar.

### Dados por domínio

Cada área cuida do próprio pedaço. Isso ajuda porque o time já fala a linguagem do negócio e sabe o que o dado significa.

Exemplo:

* vendas entende pedido, conversão e receita;
* financeiro entende faturamento, repasse e inadimplência;
* logística entende entrega, prazo e SLA.

### Dados como produto

Esse ponto é importante. O dado não pode ser só “uma tabela jogada no catálogo”.

Se ele vai ser consumido por outras equipes, precisa ter:

* dono claro;
* documentação mínima;
* contrato de uso;
* qualidade conhecida;
* expectativa de atualização;
* definição do que aquele dado representa.

Se isso não existe, o consumo vira ruído.

### Plataforma self-service

Os times de domínio precisam conseguir publicar e consumir dados sem depender de uma equipe central para cada detalhe.

Na AWS, isso geralmente passa por:

* **Amazon S3** para armazenar os dados;
* **AWS Glue Catalog** para catalogar metadados;
* **Amazon Athena** para consultas SQL;
* **AWS Lake Formation** para governança e controle de acesso;
* **AWS Glue** e **Amazon EMR** para processamento;
* **Amazon Redshift** quando a camada analítica central ainda faz sentido.

### Governança federada

Mesmo com autonomia, a empresa não pode abrir mão de padrão.

A governança entra para definir:

* quem pode publicar;
* quem pode consumir;
* como os dados são nomeados;
* quais metadados são obrigatórios;
* quais regras de segurança precisam ser seguidas.

Ou seja: cada domínio assume responsabilidade, mas não inventa tudo do zero.

---

## Onde a AWS entra nisso

Na AWS, o data mesh não depende de um serviço único. Ele é mais uma combinação de peças.

Uma forma comum de montar isso é:

<div class="mermaid">
flowchart TB
    subgraph Dominios
      A[Domínio Vendas]
      B[Domínio Marketing]
      C[Domínio Financeiro]
    end

    subgraph Plataforma
      D[Amazon S3]
      E[AWS Glue Catalog]
      F[AWS Lake Formation]
      G[Amazon Athena]
    end

    A --> D
    B --> D
    C --> D
    D --> E
    E --> F
    F --> G
</div>

Esse desenho costuma funcionar bem quando a empresa quer autonomia sem perder controle.

---

## Data Mesh vs Data Lake

Esses dois termos aparecem juntos, mas não são a mesma coisa.

O **data lake** é a base onde os dados ficam armazenados e podem ser explorados.
O **data mesh** é a forma de organizar quem cuida desses dados e como essa responsabilidade é distribuída.

Dá para ter data lake sem data mesh.
Dá para ter data mesh usando data lake como base.
Dá para combinar data mesh com lakehouse também.

### Comparação rápida

| Critério | Data Lake | Data Mesh |
| --- | --- | --- |
| Foco principal | Armazenamento e exploração | Organização por domínio |
| Responsabilidade | Mais centralizada | Distribuída por área |
| Governança | Técnica | Federada |
| Estrutura | Repositório de dados | Modelo operacional |
| AWS mais comum | S3, Glue, Athena | S3, Glue, Lake Formation, Athena, Redshift |

---

## Quando faz sentido usar

Data mesh faz sentido quando a empresa já cresceu o suficiente para ter vários domínios maduros e um time central de dados que virou gargalo.

Ele funciona melhor quando:

* existem várias áreas com autonomia real;
* os dados já têm uso importante no negócio;
* há maturidade para documentação e governança;
* a empresa aceita responsabilidade distribuída;
* a plataforma de dados já está organizada o bastante para suportar isso.

Se a empresa ainda está organizando o básico de ingestão, qualidade e catálogo, normalmente o data mesh é cedo demais. Nesse caso, faz mais sentido fortalecer o lake, o warehouse ou o lakehouse primeiro.

---

## Fechando a ideia

O jeito mais simples de pensar em data mesh é este:

* **Data Lake**: onde os dados ficam.
* **Data Warehouse**: onde os dados são organizados para análise.
* **Data Mesh**: quem é dono dos dados e como essa responsabilidade é distribuída.

Na AWS, isso costuma girar em torno de **S3**, **Glue**, **Athena**, **Lake Formation**, **EMR** e, em alguns casos, **Redshift**.

O data mesh não é uma solução mágica. Ele só faz sentido quando a empresa já tem complexidade suficiente para justificar essa distribuição de responsabilidade.
