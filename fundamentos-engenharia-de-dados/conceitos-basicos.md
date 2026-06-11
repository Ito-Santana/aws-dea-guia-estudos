---
title: Conceitos Básicos
layout: default
description: Tipos de dados, propriedades e base conceitual de engenharia de dados
---

# Conceitos Básicos de Engenharia de Dados

## Tipos de Dados

Na Engenharia de Dados, uma das primeiras classificações importantes é entender como os dados estão organizados. De forma geral, eles podem ser divididos em três categorias principais:

* Dados estruturados
* Dados semiestruturados
* Dados não estruturados

---

## Dados Estruturados

Dados estruturados são dados organizados em um formato bem definido, normalmente seguindo um esquema fixo. Eles costumam ser armazenados em tabelas, com linhas e colunas, sendo comuns em bancos de dados relacionais.

Esse tipo de dado é mais fácil de consultar, validar e relacionar, principalmente usando SQL.

### Características

* Possuem estrutura consistente
* São organizados em linhas e colunas
* Têm schema bem definido
* São facilmente consultáveis com SQL
* São comuns em sistemas transacionais e analíticos

### Exemplos

* Tabelas em bancos relacionais
* Arquivos CSV
* Planilhas Excel
* MySQL
* PostgreSQL
* Oracle
* SQL Server
* Amazon Redshift

### Exemplo prático

Uma tabela de clientes com colunas como:

```text
id_cliente | nome | email | data_cadastro
```

Nesse caso, cada registro segue a mesma estrutura.

---

## Dados Semiestruturados

Dados semiestruturados não seguem o modelo rígido de linhas e colunas, mas ainda possuem alguma organização interna. Normalmente, eles usam chaves, tags ou hierarquias para representar informações.

Esse tipo de dado é muito comum em APIs, logs, eventos e integrações entre sistemas.

### Características

* Não possuem estrutura tabular rígida
* Possuem algum padrão de organização
* Podem ter campos opcionais ou variáveis
* São comuns em sistemas distribuídos, APIs e pipelines de dados
* Podem ser processados por ferramentas como Spark, Glue, Athena e bancos NoSQL

### Exemplos

* JSON
* XML
* Avro
* Parquet
* ORC
* Logs de aplicações
* Eventos de streaming
* Respostas de APIs

### Exemplo prático

```json
{
  "id_cliente": 123,
  "nome": "Maria",
  "email": "maria@email.com",
  "enderecos": [
    {
      "cidade": "Recife",
      "estado": "PE"
    }
  ]
}
```

Esse dado não está em formato de tabela tradicional, mas possui uma estrutura clara baseada em **chaves e valores**.

---

## Dados Não Estruturados

Dados não estruturados são dados que não possuem um formato predefinido ou um schema claro. Eles geralmente exigem processamento adicional para que informações úteis possam ser extraídas.

Esse tipo de dado é comum em arquivos multimídia, documentos, textos livres e conteúdos gerados por usuários.

### Características

* Não possuem schema definido
* São mais difíceis de consultar diretamente
* Normalmente exigem pré-processamento
* Podem precisar de técnicas de NLP, visão computacional ou extração de texto
* Costumam ocupar grande volume de armazenamento

### Exemplos

* Imagens
* Vídeos
* Áudios
* PDFs
* E-mails
* Documentos de texto
* Contratos
* Posts em redes sociais
* Chamados de atendimento

### Exemplo prático

Um arquivo de áudio de uma ligação de atendimento não possui colunas ou campos estruturados. Para analisá-lo, seria necessário primeiro transcrever o áudio e depois aplicar algum processamento sobre o texto.

---

## Comparação Rápida

| Tipo de dado    | Estrutura                                           | Exemplos                               | Facilidade de consulta |
| --------------- | --------------------------------------------------- | -------------------------------------- | ---------------------- |
| Estruturado     | Schema fixo, linhas e colunas                       | SQL, CSV, PostgreSQL, Redshift         | Alta                   |
| Semiestruturado | Organização flexível com chaves, tags ou hierarquia | JSON, XML, Logs, Avro, Parquet         | Média                  |
| Não estruturado | Sem schema definido                                 | Imagens, vídeos, áudios, PDFs, e-mails | Baixa                  |

---

# Propriedade dos Dados (3V's)

## Volume

Volume se refere à quantidade de dados que uma empresa ou sistema precisa armazenar e processar. Esse volume pode variar bastante, indo de gigabytes até terabytes, petabytes ou mais.

Quando o volume cresce, alguns desafios começam a aparecer:

- como armazenar esses dados de forma eficiente;
- como processar sem demorar demais;
- como evitar custos desnecessários;
- como organizar os dados para facilitar consultas futuras.

Exemplo:

Uma rede social pode gerar terabytes de dados por dia com posts, curtidas, comentários, imagens, vídeos e logs de navegação dos usuários.

---

## Velocidade

Velocidade se refere à rapidez com que novos dados são gerados, coletados e precisam ser processados.

Nem todo dado precisa ser processado em tempo real. Alguns dados podem ser processados uma vez por dia, enquanto outros precisam ser analisados em poucos segundos.

Quando a velocidade é alta, normalmente entram arquiteturas de streaming ou processamento quase em tempo real.

Exemplo:

Um sistema antifraude precisa analisar transações financeiras quase em tempo real. Se a análise demorar muito, a transação suspeita pode ser aprovada antes da detecção.

---

## Variedade

Variedade se refere aos diferentes formatos e origens dos dados.

Na prática, uma empresa raramente trabalha com apenas um tipo de dado. Ela pode receber dados de bancos relacionais, APIs, arquivos CSV, logs, eventos, imagens, vídeos e documentos.

Essa variedade traz desafios porque cada fonte pode ter um formato, um schema e uma qualidade diferente.

Exemplos de formatos:

- CSV;
- JSON;
- imagens;
- vídeos;
- arquivos de texto;
- logs de aplicação.

Exemplo:

Uma empresa de e-commerce pode ter dados de pedidos em um banco relacional, eventos de navegação em JSON, imagens de produtos em arquivos e logs da aplicação em texto.

Antes de analisar tudo junto, é preciso organizar, padronizar e transformar esses dados.
