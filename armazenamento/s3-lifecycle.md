---

title: S3 - Lifecycle
layout: default
description: Regras de ciclo de vida no Amazon S3 para transição, expiração e controle de custo
---

# S3 - Lifecycle

## Visão Geral

`S3 Lifecycle` é o recurso usado para automatizar o ciclo de vida dos objetos no `Amazon S3`.É muito útil porque nem todo dado precisa ficar para sempre em `S3 Standard`.

Um arquivo recém-chegado pode ser acessado bastante nos primeiros dias. Depois de alguns meses, talvez vire apenas histórico. Depois de alguns anos, pode ser só retenção regulatória.

Em vez de mover ou apagar esses objetos manualmente, você cria regras de Lifecycle.

---

## O que uma regra de Lifecycle pode fazer

Uma regra de Lifecycle normalmente faz dois tipos de ação:

| Ação      | Ideia                                            |
| --------- | ------------------------------------------------ |
| Transição | Move o objeto para outra classe de armazenamento |
| Expiração | Remove o objeto depois de um período             |

Exemplo simples:

```text
após 30 dias -> mover para S3 Standard-IA
após 90 dias -> mover para S3 Glacier Flexible Retrieval
após 365 dias -> excluir
```

A lógica é reduzir custo sem depender de alguém lembrando de limpar o bucket manualmente.

---

## Transição

Transição é quando o S3 move um objeto para outra classe de armazenamento.

Exemplo:

```text
S3 Standard -> S3 Standard-IA -> S3 Glacier Flexible Retrieval
```

Isso faz sentido quando o dado vai ficando menos acessado com o tempo.

Exemplo em data lake:

```text
dados recentes -> S3 Standard
dados antigos -> S3 Standard-IA
dados históricos -> Glacier
```

Para a prova, pense assim:

```text
transição = mudar classe de armazenamento
```

---

## Expiração

Expiração é quando o S3 remove objetos automaticamente depois de um período definido.

Exemplo:

```text
logs temporários devem ser excluídos depois de 90 dias
```

Isso é comum para:

* logs antigos;
* arquivos temporários;
* resultados intermediários;
* dados que já passaram do período de retenção;
* objetos que não precisam ser mantidos para sempre.

Para a prova, pense assim:

```text
expiração = apagar objeto automaticamente
```

Um detalhe: a remoção por Lifecycle pode não ser instantânea no exato segundo em que o objeto expira. O S3 avalia e executa essas ações de forma assíncrona. A documentação da AWS menciona que pode haver atraso entre a data de expiração e a remoção real do objeto.

---

## Filtros da regra

Você não precisa aplicar Lifecycle no bucket inteiro.

A regra pode ser limitada por critérios como:

* prefixo;
* tags;
* tamanho do objeto;
* combinação de filtros.

Exemplo por prefixo:

```text
logs/ -> excluir depois de 90 dias
curated/ -> manter por mais tempo
tmp/ -> excluir depois de 7 dias
```

Exemplo por tag:

```text
retencao=curta -> excluir depois de 30 dias
retencao=longa -> mover para Glacier depois de 180 dias
```

Esse ponto é importante porque em data lake nem toda camada tem o mesmo ciclo de vida.

---

## Lifecycle e versionamento

Quando o bucket tem versionamento habilitado, Lifecycle fica ainda mais importante.

Isso porque versões antigas continuam armazenadas e podem aumentar custo.

Com Lifecycle, você pode criar regras para:

* mover versões antigas para classes mais baratas;
* excluir versões antigas depois de certo tempo;
* remover delete markers expirados.

Exemplo:

```text
versões atuais -> manter em Standard
versões antigas -> mover para Standard-IA após 30 dias
versões antigas -> excluir após 180 dias
```

A AWS tem ações específicas para expirar versões não atuais de objetos em buckets com versionamento habilitado.

---

## Relação com classes de armazenamento

Lifecycle e classes de armazenamento andam juntos.

A classe define onde o objeto está armazenado.

Lifecycle define quando ele muda de classe ou quando expira.

Exemplo:

```text
S3 Standard -> acesso frequente
S3 Standard-IA -> pouco acesso
S3 Glacier Flexible Retrieval -> arquivamento
S3 Glacier Deep Archive -> retenção longa
```

Uma regra comum:

```text
0 a 30 dias -> S3 Standard
30 a 90 dias -> S3 Standard-IA
90+ dias -> Glacier
```

---

## Atenção para a prova

* Lifecycle é configurado por bucket.
* Uma regra pode usar prefixo, tags e tamanho do objeto.
* Transição muda a classe de armazenamento.
* Expiração remove objetos.
* Lifecycle ajuda a reduzir custo.
* Lifecycle pode trabalhar com versões antigas em buckets versionados.
* Pode remover delete markers expirados.
* Classes mais baratas podem ter custo de recuperação.
* Algumas classes têm duração mínima de armazenamento.
* Não aplique regra no bucket inteiro se só um prefixo deveria ser afetado.
* Lifecycle não é backup; é automação de retenção, transição e exclusão.

---

## Resumo rápido

`S3 Lifecycle` automatiza o que acontece com objetos ao longo do tempo.

Ele pode mover objetos para classes mais baratas ou excluir objetos depois de um período.

Em data lake, ajuda a controlar custo em dados antigos, logs, arquivos temporários e versões antigas.

Para a prova, lembre:

```text
transição = mudar storage class
expiração = excluir objeto
filtros = prefixo, tags e tamanho
versionamento = cuidado com versões antigas e delete markers
```

---
