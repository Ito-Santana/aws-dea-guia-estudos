---

title: DynamoDB - Modos de Capacidade
layout: default
description: Modos de capacidade do Amazon DynamoDB com foco em On-Demand, Provisioned, RCU, WCU e consistência de leitura
---

# DynamoDB - Modos de Capacidade

## Visão Geral

No `Amazon DynamoDB`, modo de capacidade define como a tabela lida com leitura e escrita.

Existem dois modos principais:

| Modo          | Ideia                                         |
| ------------- | --------------------------------------------- |
| `On-Demand`   | A AWS ajusta a capacidade conforme o uso      |
| `Provisioned` | Você define a capacidade de leitura e escrita |


---

## On-Demand

No modo `On-Demand`, você não precisa definir previamente quantas leituras e escritas a tabela vai suportar.

A tabela se ajusta automaticamente conforme o tráfego.

Esse modo é bom quando você não sabe o volume de acesso ou quando a aplicação tem picos imprevisíveis.

Exemplos:

```text
aplicação nova sem histórico de uso
campanha com pico inesperado
API com tráfego variável
ambiente de teste ou desenvolvimento
```


Você cria a tabela e não precisa ficar calculando `RCU` e `WCU` antes.

A desvantagem é que, em cargas muito previsíveis e constantes, pode sair mais caro do que provisionar capacidade corretamente.


---

## Provisioned

No modo `Provisioned`, você informa quanta capacidade de leitura e escrita quer reservar para a tabela.

Aqui entram dois conceitos importantes:

```text
RCU -> Read Capacity Unit
WCU -> Write Capacity Unit
```

Esse modo faz sentido quando o tráfego é mais previsível.

Exemplos:

```text
aplicação com padrão de acesso conhecido
sistema com volume estável
workload onde custo previsível é importante
```

A vantagem é ter mais controle de custo e capacidade.

A desvantagem é que você precisa dimensionar melhor.

Se provisionar pouco, pode ocorrer throttling.

Se provisionar demais, você paga por capacidade que talvez não use.


---

## RCU

`RCU` significa `Read Capacity Unit`.

Ela mede capacidade de leitura.

A regra base é:

```text
1 RCU = 1 leitura fortemente consistente por segundo de até 4 KB
```

Ou:

```text
1 RCU = 2 leituras eventualmente consistentes por segundo de até 4 KB
```

Então, se o item tem até `4 KB`:

| Tipo de leitura            | Consumo |
| -------------------------- | ------- |
| Strongly consistent read   | 1 RCU   |
| Eventually consistent read | 0,5 RCU |

Isso significa que leitura eventualmente consistente custa metade da leitura fortemente consistente.

---

## WCU

`WCU` significa `Write Capacity Unit`.

Ela mede capacidade de escrita.

A regra base é:

```text
1 WCU = 1 escrita por segundo de até 1 KB
```

Se o item for maior que `1 KB`, o DynamoDB arredonda para cima.

Exemplo:

| Tamanho do item       | Consumo por escrita |
| --------------------- | ------------------- |
| Até 1 KB              | 1 WCU               |
| Mais de 1 KB até 2 KB | 2 WCUs              |
| Mais de 2 KB até 3 KB | 3 WCUs              |

Para a prova, guarde:

```text
WCU usa blocos de 1 KB
RCU usa blocos de 4 KB
```

---

## Como calcular RCU

Para calcular RCU, você olha três coisas:

```text
tamanho do item
quantidade de leituras por segundo
tipo de consistência
```

A base é sempre bloco de `4 KB`.

### Leitura fortemente consistente

Uma leitura fortemente consistente de um item até `4 KB` consome `1 RCU`.

Exemplo:

```text
Item de 4 KB
10 leituras fortemente consistentes por segundo
```

Cálculo:

```text
10 x 1 RCU = 10 RCUs
```

Outro exemplo:

```text
Item de 8 KB
10 leituras fortemente consistentes por segundo
```

Como `8 KB` ocupa dois blocos de `4 KB`:

```text
2 blocos x 10 leituras = 20 RCUs
```

---

## Como calcular Eventually Consistent Read

Leitura eventualmente consistente consome metade.

Uma leitura eventualmente consistente de um item até `4 KB` consome `0,5 RCU`.

Exemplo:

```text
Item de 4 KB
10 leituras eventualmente consistentes por segundo
```

Cálculo:

```text
10 x 0,5 RCU = 5 RCUs
```

Outro exemplo:

```text
Item de 8 KB
10 leituras eventualmente consistentes por segundo
```

Como `8 KB` ocupa dois blocos de `4 KB`:

```text
2 blocos x 10 leituras x 0,5 = 10 RCUs
```

Para a prova, pense:

```text
eventually consistent read = metade do custo de leitura
```

---

## Strongly Consistent Read

`Strongly consistent read` é uma leitura que tenta retornar o dado mais atualizado.

Se uma escrita foi concluída com sucesso antes da leitura, a leitura fortemente consistente deve refletir essa escrita.

Use quando a aplicação precisa ler o valor mais recente possível.

Exemplo:

```text
usuário acabou de atualizar o saldo
a próxima leitura precisa mostrar o saldo atualizado
```

A desvantagem é que consome mais capacidade.

Para a prova:

```text
strongly consistent = mais atual, consome mais RCU
```

---

## Eventually Consistent Read

`Eventually consistent read` é o padrão de leitura do DynamoDB.

Ela pode não refletir imediatamente uma escrita recém-concluída.

Mas, se você repetir a leitura pouco tempo depois, a tendência é que o valor atualizado apareça.

Exemplo:

```text
usuário atualizou um dado
uma leitura logo em seguida pode ver o valor antigo por pouco tempo
```

A vantagem é que custa menos capacidade de leitura.

Para a prova:

```text
eventually consistent = pode atrasar um pouco, consome menos RCU
```

---

## Comparação rápida

| Tipo de leitura              | Atualização do dado                              | Consumo |
| ---------------------------- | ------------------------------------------------ | ------- |
| `Strongly consistent read`   | Retorna dado mais atualizado                     | Maior   |
| `Eventually consistent read` | Pode demorar pouco para refletir escrita recente | Menor   |


---

## Como calcular WCU

Para calcular WCU, você olha:

```text
tamanho do item
quantidade de escritas por segundo
```

A base é bloco de `1 KB`.

Exemplo:

```text
Item de 1 KB
20 escritas por segundo
```

Cálculo:

```text
20 x 1 WCU = 20 WCUs
```

Outro exemplo:

```text
Item de 3 KB
20 escritas por segundo
```

Como `3 KB` ocupa três blocos de `1 KB`:

```text
3 blocos x 20 escritas = 60 WCUs
```

Para a prova:

```text
escrita arredonda de 1 em 1 KB
```

---

## Throttling

`Throttling` acontece quando a aplicação tenta consumir mais capacidade do que a tabela consegue atender naquele momento.

No modo `Provisioned`, isso pode acontecer se você configurar pouca capacidade.

Exemplo:

```text
tabela provisionada para 100 leituras por segundo
aplicação tenta fazer 500 leituras por segundo
```

Resultado:

```text
algumas requisições podem ser limitadas
```

Para lidar com isso, você pode:

* aumentar `RCU` ou `WCU`;
* usar auto scaling;
* revisar a partition key;
* mudar para On-Demand em cenários imprevisíveis;
* usar retry com backoff na aplicação.

Para a prova, guarde:

```text
throttling = consumo acima da capacidade disponível
```

---

## Auto Scaling

No modo `Provisioned`, você pode usar auto scaling para ajustar `RCU` e `WCU`.

A ideia é aumentar ou reduzir a capacidade conforme o uso.

Exemplo:

```text
durante o dia -> mais tráfego -> aumenta capacidade
de madrugada -> menos tráfego -> reduz capacidade
```

Isso ajuda a equilibrar custo e performance.

Para a prova:

```text
Provisioned + Auto Scaling = capacidade ajustada conforme utilização
```

---

## On-Demand vs Provisioned

| Critério                | On-Demand                | Provisioned               |
| ----------------------- | ------------------------ | ------------------------- |
| Capacidade              | Ajustada automaticamente | Definida por você         |
| Melhor para             | Tráfego imprevisível     | Tráfego previsível        |
| Simplicidade            | Maior                    | Menor                     |
| Controle de custo       | Menor em carga constante | Maior se bem dimensionado |
| Risco de subprovisionar | Menor                    | Maior                     |
| Conceitos principais    | Request units            | RCU e WCU                 |

---
