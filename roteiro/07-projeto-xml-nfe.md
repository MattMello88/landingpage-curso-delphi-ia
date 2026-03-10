# BLOCO 7 — O PROJETO: Leitura de XML de NF-e (10–12 min)

[← Bloco 6 — Skills e Prompts](06-skills-prompts-delphi.md) | **[Índice](../README.md)** | [Próximo: Bloco 8 — Formulários →](08-gerando-formularios.md)

---

**Objetivo:** Coração do vídeo — aplicação real

> 📋 **Prompts prontos:** Use o arquivo [prompt-projeto-delphi-xml-nfe.md](prompt-projeto-delphi-xml-nfe.md) para copiar prompts completos (análise XML, DDL, importação, formulários).

## Parte 6a — Analisando o XML
- Abrir um XML de NF-e real (ou de exemplo público)
- Conversar com o Cursor: *"Analise esse XML e me liste os grupos de tags e seus atributos"*
- Ver a IA mapear: `<ide>`, `<emit>`, `<dest>`, `<det>`, `<total>`, `<transp>`, etc.

## Parte 6b — Gerando as Tabelas
- Prompt para geração de DDL:
  > *"Com base na análise do XML, gere os scripts SQL para criar as tabelas no Firebird/PostgreSQL/SQL Server [escolher], com os tipos de dados corretos para cada campo"*
- Revisar o SQL gerado, mostrar como corrigir/ajustar com novos prompts
- Executar os scripts

## Parte 6c — Código de Importação em Delphi
- Prompt: *"Crie uma unit Delphi para ler o XML de NF-e usando TXMLDocument e popular as tabelas via FireDAC"*
- Revisar o código gerado
- Mostrar ajustes finos (tratamento de erros, campos opcionais)
- Testar a importação

---

[← Bloco 6 — Skills e Prompts](06-skills-prompts-delphi.md) | **[Índice](../README.md)** | [Próximo: Bloco 8 — Formulários →](08-gerando-formularios.md)
