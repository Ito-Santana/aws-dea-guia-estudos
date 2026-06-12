---
title: AWS Backup - Conceitos
layout: default
description: Conceitos básicos do AWS Backup, planos de backup, vaults, retenção e restauração para estudo da AWS DEA-C01
---

# AWS Backup - Conceitos

## Visão Geral

`AWS Backup` é um serviço gerenciado para centralizar e automatizar backups de recursos da AWS.

Em vez de configurar backup separadamente em cada serviço, você cria políticas em um lugar só e aplica essas regras aos recursos protegidos.

Para a `DEA-C01`, pense nele como uma camada de governança operacional para backup, retenção e restauração.

```text
Recursos da AWS -> plano de backup -> backup vault -> pontos de recuperação
```

---

## Conceitos principais

### Backup plan

Um `backup plan` define a política de backup.

Ele pode controlar:

- frequência do backup;
- janela de execução;
- período de retenção;
- ciclo de vida;
- cópia para outra região ou conta;
- recursos protegidos.

### Backup vault

Um `backup vault` é o cofre onde os pontos de recuperação ficam armazenados.

Ele ajuda a organizar, controlar acesso e aplicar proteção aos backups.

### Recovery point

Um `recovery point` representa um backup disponível para restauração.

É a partir dele que você recupera um recurso para um estado anterior.

---

## Resumo rápido

- `AWS Backup` centraliza políticas de backup.
- `Backup plan` define frequência, retenção e ciclo de vida.
- `Backup vault` armazena e protege pontos de recuperação.
- `Recovery point` é o backup usado para restauração.
- É útil para governança, auditoria e recuperação operacional.
---