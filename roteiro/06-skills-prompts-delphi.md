# BLOCO 6 — Skills e Prompts para Delphi (5–6 min)

[← Bloco 5 — Rules e Guidelines](05-rules-guidelines.md) | **[Índice](../README.md)** | [Próximo: Bloco 7 — Projeto XML NF-e →](07-projeto-xml-nfe.md)

---

**Objetivo:** Ensinar a "falar a língua certa" com a IA — contexto certo + prompts eficientes

---

## Parte 6a — Skills e arquivos de contexto

### O que são Skills no Cursor

- **Skills** = pastas com `SKILL.md` (YAML frontmatter + instruções) em `.cursor/skills/` ou `~/.cursor/skills/`
- A IA usa a *description* do Skill para decidir **quando** aplicá-lo automaticamente
- **Arquivos `.md` ou `.mdc`** = podem ser referenciados manualmente com `@` no chat (ex.: `@delphi-nomenclatura.mdc`)

### Quando usar cada um

| Recurso | Uso | Exemplo |
|---------|-----|---------|
| **Rules** (`.cursor/rules/*.mdc`) | Aplicadas automaticamente em todo o projeto | `delphi-nomenclatura.mdc`, `delphi-cadastro-base.mdc` |
| **Arquivo de contexto** (`@arquivo.md`) | Injetar contexto específico em uma conversa | `@roteiro/prompt-projeto-delphi-xml-nfe.md` |
| **Skills** (`.cursor/skills/nome/SKILL.md`) | Workflows especializados que a IA aplica quando detecta o cenário | Ex.: skill para análise de XML |

### Criar um arquivo de contexto para Delphi

Crie `delphi.md` (ou use as Rules já existentes) com:

- **Stack do projeto:** Delphi XE10, FireDAC, dbExpress, etc.
- **Padrões de nomenclatura:** Tfrm, Tdm, btn, ed, qry, ds (ver Bloco 5)
- **Convenções:** ancestral para cadastro, mestre-detalhe, uso de Excel

> 💡 **Dica:** O projeto já tem Rules em `.cursor/rules/` — use `@delphi-nomenclatura.mdc` nos prompts quando quiser reforçar o contexto.

---

## Parte 6b — Bons prompts vs. prompts fracos

### Por que o prompt importa

- Prompts vagos → respostas genéricas ou incorretas
- Prompts específicos → código alinhado ao seu projeto, menos retrabalho

### Exemplos práticos

| ❌ Fraco | ✅ Bom |
|----------|--------|
| *"Cria uma tabela"* | *"Analisa o XML de NF-e anexo e cria scripts SQL para cada grupo de tags (ide, emit, dest, det, total), seguindo as convenções @delphi-nomenclatura.mdc"* |
| *"Faz um formulário"* | *"Crie um formulário de cadastro de cliente herdando de TfrmCadastroBase, com campos Nome, CPF, Email e DataNascimento. Use FireDAC e siga os prefixos btn/ed/lbl."* |
| *"Importa o XML"* | *"Crie uma unit Delphi para ler o XML de NF-e com TXMLDocument e popular as tabelas NFE_CABECALHO e NFE_ITEM via FireDAC. Trate campos opcionais e registre erros em log."* |

### Fórmula de um bom prompt

1. **Contexto** — o que você tem (arquivo anexo, schema, convenções)
2. **Ação** — o que a IA deve fazer (analisar, criar, refatorar)
3. **Restrições** — tecnologias, padrões, formato de saída
4. **Referências** — `@arquivo` ou `@rule` quando aplicável

---

## Parte 6c — Referenciar contexto no chat

- Digite `@` e escolha: arquivo, pasta, Rule ou Skill
- Ex.: `@delphi-nomenclatura.mdc` ou `@roteiro/prompt-projeto-delphi-xml-nfe.md`
- A IA passa a considerar esse conteúdo na resposta

---

### Resumo para a gravação

1. Explicar diferença entre Skills, Rules e arquivos de contexto.
2. Mostrar o que colocar em um `delphi.md` (ou usar as Rules existentes).
3. Contrastar prompts fracos vs. bons com exemplos reais (tabela, formulário, importação XML).
4. Ensinar a fórmula: contexto + ação + restrições + referências.
5. Demonstrar o uso de `@` para injetar contexto.

---

[← Bloco 5 — Rules e Guidelines](05-rules-guidelines.md) | **[Índice](../README.md)** | [Próximo: Bloco 7 — Projeto XML NF-e →](07-projeto-xml-nfe.md)
