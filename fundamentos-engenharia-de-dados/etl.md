---
title: ETL
layout: default
description: Extract, Transform, Load no contexto de pipelines de dados na AWS
---

# ETL

## Visão Geral

ETL significa `Extract, Transform, Load`.

É o fluxo em que você extrai os dados da origem, transforma antes e só depois carrega no destino final.

Isso continua sendo um conceito básico porque dado de origem quase nunca chega pronto. Sempre tem alguma coisa para ajustar: tipo, nulo, duplicidade, regra de negócio, schema, formato.

## Por que isso importa em Engenharia de Dados?

Porque boa parte do trabalho de engenharia de dados é exatamente pegar dado operacional e deixá-lo utilizável.

Sem ETL, ou sem alguma variação dele, você acaba espalhando dado inconsistente pela arquitetura.

## Etapas do ETL

## Extract

É a captura da origem.

Pode vir de:

- `Amazon RDS`;
- `Amazon DynamoDB`;
- APIs;
- arquivos no `S3`;
- logs;
- eventos.

## Transform

Aqui mora a parte mais trabalhosa.

É onde você:

- corrige tipos;
- padroniza datas;
- remove duplicidade;
- trata nulos;
- aplica regra de negócio;
- faz join;
- enriquece;
- converte formato, por exemplo de `CSV` para `Parquet`.

## Load

Depois de tratar, você grava o resultado onde ele será consumido.

Destinos comuns:

- `Amazon S3`;
- `Amazon Redshift`;
- tabelas para `Athena`;
- camadas curadas para outros times.

## Como aparece na AWS

Na AWS, ETL aparece muito com:

- `AWS Glue`;
- `Amazon EMR`;
- `Amazon S3`;
- `Amazon Redshift`;
- `Amazon Athena`;
- `AWS Step Functions` e `Amazon EventBridge` para orquestração.

Se a questão pedir ETL gerenciado e serverless, `AWS Glue` é um candidato muito forte.

## Exemplo prático

Chegam arquivos CSV de vendas no `S3`.

O job no `Glue`:

- lê os arquivos;
- corrige tipos;
- remove registros inválidos;
- padroniza timestamp;
- converte para `Parquet`;
- grava a camada curada no `S3`;
- publica a tabela no catálogo para consulta via `Athena`.

```mermaid
flowchart LR
    A[CSV no S3] --> B[AWS Glue]
    B --> C[Tratamento e padronizacao]
    C --> D[Parquet curado no S3]
    D --> E[AWS Glue Data Catalog]
    E --> F[Amazon Athena]
```

## ETL vs ELT

Essa diferença cai bastante:

- `ETL`: transforma antes de carregar;
- `ELT`: carrega antes e transforma depois no destino.

Se o destino analítico tem força para transformar depois, `ELT` pode ser uma escolha melhor. Se o dado precisa chegar já controlado e limpo, `ETL` faz bastante sentido.

## Pegadinhas para a prova

- `Glue` é muito associado a ETL na AWS;
- `Lambda` pode transformar, mas não é escolha natural para ETL pesado;
- converter para `Parquet` costuma melhorar leitura analítica;
- ETL e ingestão não são exatamente a mesma coisa.

## Quando usar

- quando o dado precisa ser tratado antes do consumo;
- quando a qualidade precisa ser controlada cedo;
- quando existem regras claras de negócio antes da carga final.

## Quando não usar

- quando a ideia é só aterrissar dado bruto rapidamente;
- quando o modelo é claramente `ELT`;
- quando a transformação é mínima e cabe melhor no motor de consulta.

## Comparação com conceitos parecidos

| Conceito | Ideia |
| --- | --- |
| ETL | Extrai, transforma, carrega |
| ELT | Extrai, carrega, transforma |
| CDC | Captura mudança na origem |
| Ingestão | Coloca o dado no pipeline |

## Resumo rápido

- ETL organiza a entrada do dado antes do destino final.
- `Glue`, `S3`, `Athena`, `EMR` e `Redshift` aparecem muito nesse assunto.
- Para a prova, diferenciar ETL de ELT é essencial.

## Checklist para prova

- [ ] Saber a ordem do ETL
- [ ] Diferenciar ETL de ELT
- [ ] Associar ETL a limpeza e padronização
- [ ] Lembrar de `AWS Glue`
- [ ] Relacionar `Parquet` com camada analítica no lake
