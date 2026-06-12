---

title: Amazon EBS - Conceitos
layout: default
description: Conceitos básicos do Amazon Elastic Block Store, volumes EBS e tipos de volume para estudo da AWS DEA-C01
---

# Amazon EBS - Conceitos

## Visão Geral

`Amazon EBS` significa **Amazon Elastic Block Store**.

Ele é o serviço de armazenamento em bloco usado principalmente com instâncias `Amazon EC2`.O EBS é tipo um “disco” que você anexa a uma instância EC2.

Depois que o volume é anexado, a instância consegue usar esse volume como se fosse um disco local: formatar, montar, gravar arquivos, instalar aplicações ou armazenar dados de banco.

A própria AWS define um volume EBS como um dispositivo de armazenamento em bloco durável que pode ser anexado a instâncias EC2. Depois de anexado, ele pode ser usado como um disco físico.
---

## O que é armazenamento em bloco?

Armazenamento em bloco é um tipo de storage em que os dados são gravados em blocos.

Esse modelo é diferente do `Amazon S3`.

No `S3`, você armazena objetos, como arquivos completos.

No `EBS`, você fornece um volume em bloco para uma máquina usar como disco.


Exemplo:

```text
EC2 precisa de disco para sistema operacional, aplicação ou banco local -> EBS
```

---

## Volume EBS

Um `EBS volume` é o volume de armazenamento criado dentro do Amazon EBS.

Ele pode ser anexado a uma instância EC2 e usado como disco.


```text
Instância EC2: servidor-aplicacao
Volume EBS: 100 GB gp3
Uso: armazenar arquivos da aplicação
```

Depois de anexar um volume à instância, ele aparece como um dispositivo de bloco. Você pode formatar o volume com um sistema de arquivos e montar para uso.

Um ponto importante: o volume EBS é independente do ciclo de vida da instância.

Ou seja, dependendo da configuração, você pode parar ou encerrar uma instância e manter o volume existindo.


---

## EBS e zona de disponibilidade

Um volume EBS é criado em uma zona de disponibilidade específica.

Isso é importante porque ele precisa estar na mesma `Availability Zone` da instância EC2 para ser anexado.

Se a instância estiver em outra zona, você não anexa diretamente aquele volume.

Para mover dados entre zonas, normalmente você usa snapshot e cria outro volume na zona desejada.

---

## Snapshots

Snapshot é uma cópia de backup de um volume EBS.

Os snapshots são armazenados no `Amazon S3`, mas você não acessa esses arquivos diretamente como objetos comuns.

Eles servem para:

* backup;
* recuperação;
* criação de novos volumes;
* cópia de volume entre regiões;
* mover dados entre zonas de disponibilidade.


---

## Elastic Volumes

Com `Elastic Volumes`, você pode modificar algumas características de um volume EBS.

Por exemplo:

* aumentar tamanho;
* mudar tipo de volume;
* ajustar performance.

A AWS permite aumentar tamanho, alterar tipo de volume ou ajustar performance em volumes EBS, em muitos casos sem desanexar o volume ou reiniciar a instância.

Exemplo:

```text
Volume gp2 de 100 GB -> alterar para gp3 de 200 GB
```

---

## Exemplo prático

Imagine uma aplicação rodando em uma instância EC2.

Ela precisa de:

* disco para o sistema operacional;
* armazenamento para arquivos da aplicação;
* baixa latência;
* persistência mesmo se a instância for parada.

Nesse caso, `Amazon EBS` faz sentido.

```mermaid
flowchart LR
    A[Amazon EC2] --> B[Volume EBS gp3]
    B --> C[Sistema de arquivos]
    C --> D[Aplicacao ou banco]
```

Se a aplicação precisar de uma cópia de segurança, você cria snapshots do volume.

```mermaid
flowchart LR
    A[Volume EBS] --> B[Snapshot]
    B --> C[Novo volume EBS]
```


---

## Resumo rápido

`Amazon EBS` é armazenamento em bloco para `Amazon EC2`.

Um volume EBS funciona como um disco anexado à instância.

Ele é útil para sistema operacional, aplicações, bancos e workloads que precisam de baixa latência.

Para a prova, lembre:

```text
EBS = bloco + EC2 + volume + AZ + snapshot
```

---
