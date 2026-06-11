# Guia Local da Sessão

Este arquivo é local e serve como memória de trabalho do projeto. Ele não deve aparecer no GitHub Pages nem ser versionado no repositório.

## Objetivo do projeto

Disponibilizar uma trilha de estudo para a prova `AWS Certified Data Engineer - Associate (DEA-C01)` em formato de documentação navegável.

A ideia não é só guardar anotações. O objetivo é transformar estudo técnico em material organizado, revisável e útil para consulta posterior.

## Direção editorial

O conteúdo do site deve:

- ser técnico, mas humano;
- evitar cara de texto genérico de IA;
- conectar os assuntos com engenharia de dados na AWS;
- focar no que ajuda de verdade na `DEA-C01`;
- usar exemplos práticos;
- destacar pegadinhas de prova;
- evitar propaganda da AWS e frases vazias.

## Estrutura esperada para páginas

Sempre que fizer sentido, usar algo próximo de:

- `Visão Geral`
- `Por que isso importa em Engenharia de Dados?`
- `Como aparece na AWS`
- `Exemplo prático`
- `Pegadinhas para a prova`
- `Quando usar`
- `Quando não usar`
- `Comparação com conceitos parecidos`
- `Diagrama`
- `Resumo rápido`
- `Checklist para prova`

Mermaid deve ser usado quando realmente ajuda a entender pipeline, arquitetura, fluxo ou distribuição.

## Decisões importantes já tomadas

### Conteúdo

Foram revisadas e reescritas várias páginas com linguagem mais humana e menos artificial, especialmente em:

- `fundamentos-engenharia-de-dados`
- `armazenamento/s3-introducao.md`

Também foi reforçado que o site deve funcionar como trilha de estudo para a `AWS DEA-C01`, não só como repositório de notas.

### Home e README

A apresentação do projeto foi melhorada para:

- explicar a ideia do guia;
- deixar claro que o material foi feito por Ítalo Santana;
- destacar que o autor é `AWS Certified` e `Databricks Certified`;
- incluir links importantes da AWS;
- incluir links do GitHub e LinkedIn.

### Navegação do site

O layout foi aproximado do estilo de documentação:

- topo mais limpo;
- sidebar fixa;
- navegação por seções;
- páginas índice por trilha;
- links de anterior/próximo;
- grupos retráteis na sidebar.

As seções atuais da navegação são:

- `Fundamentos de Engenharia de Dados`
- `Armazenamento`

### Tema e visual

O site hoje tem:

- tema claro;
- tema escuro;
- toggle manual de claro/escuro;
- persistência da escolha no navegador.

Também houve ajustes para melhorar:

- contraste do tema escuro;
- leitura de Mermaid no escuro;
- controle visual da sidebar;
- renderização de imagens dentro dos artigos.

## Estado atual do layout

### O que já funciona

- sidebar retrátil por seção;
- toggle manual de tema;
- Mermaid adaptando ao tema claro/escuro;
- imagens em artigos limitadas ao container;
- `guia.md` excluído do Jekyll e agora ignorado pelo Git;
- apresentação da home mais autoral.

### Pontos de atenção

- revisar se o toggle visual ainda pode ficar melhor;
- revisar contraste final do dark mode em uso real;
- validar se todos os Mermaid continuam bons após troca de tema;
- validar se o Pages não está cacheando visual antigo.

## Regras técnicas úteis para futuras alterações

- preferir navegação estável a geração dinâmica frágil no GitHub Pages;
- se imagem “explodir” no artigo, garantir `max-width: 100%` no CSS;
- se Mermaid perder contraste, ajustar a renderização pelo tema e não só pelo CSS;
- evitar soluções improvisadas de logo com imagem ruim;
- manter o site com cara de documentação, não landing page.

## Próximos passos sugeridos

### Conteúdo

- expandir `Armazenamento` com:
  - `S3 versioning`
  - `S3 lifecycle`
  - `S3 storage classes`
  - `prefixos e particionamento no S3`
- criar trilhas novas para:
  - `AWS Glue`
  - `Athena`
  - `Redshift`
  - `EMR`
  - `Kinesis`
  - `Lake Formation`
  - `IAM e KMS`

### Navegação e UX

- considerar busca local;
- revisar se a sidebar pode abrir apenas uma seção por vez;
- considerar um sumário por headings na lateral direita;
- revisar o visual do toggle claro/escuro;
- revisar a apresentação da home para manter concisão.

### Qualidade do material

- revisar o restante dos `.md` para manter consistência de tom;
- verificar páginas com imagens externas;
- verificar se as páginas mais longas estão bem escaneáveis;
- manter foco em revisão de prova e não em detalhamento excessivo fora da DEA-C01.

## Links do autor

- LinkedIn: `https://www.linkedin.com/in/italo-santana-26bb94255/`
- GitHub: `https://github.com/Ito-Santana`

## Observação final

Este arquivo é para contexto local da sessão. Ele deve continuar fora do versionamento e fora do GitHub Pages.
