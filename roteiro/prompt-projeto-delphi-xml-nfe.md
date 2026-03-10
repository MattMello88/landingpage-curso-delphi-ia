# Prompt Completo — Projeto Delphi Gestão XML NF-e

> **Uso:** Copie e cole este prompt no Cursor para iniciar ou evoluir o projeto de importação e gestão de XML de NF-e. Ajuste os trechos entre colchetes `[...]` conforme seu ambiente.

---

## PROMPT 1 — Análise do XML e Mapeamento

```
Analise o arquivo XML de NF-e que anexei e me liste:

1. **Grupos principais de tags** e seus atributos (ide, emit, dest, det, total, transp, cobr, pag, infAdic)
2. **Estrutura hierárquica** — quais tags são filhas de quais
3. **Campos obrigatórios vs opcionais** em cada grupo
4. **Tipos de dados** sugeridos para cada campo (string, decimal, data, inteiro)

Referência do schema: NF-e Layout v4.00 (namespace http://www.portalfiscal.inf.br/nfe).
Se não tiver o XML, use o schema XSD do ACBr: leiauteNFe_v4.00.xsd
```

---

## PROMPT 2 — Geração das Tabelas (DDL)

```
Com base na análise do XML/schema da NF-e v4, gere os scripts SQL para criar as tabelas no [Firebird / PostgreSQL / SQL Server].

**Requisitos obrigatórios:**

1. **Snapshots para emitente e destinatário**
   - Crie as tabelas NFE_EMITENTE_SNAPSHOT e NFE_DESTINATARIO_SNAPSHOT
   - Elas armazenam os dados do emitente e destinatário NO MOMENTO DA EMISSÃO da nota
   - Motivo: cadastros mudam (razão social, endereço, IE). Se referenciarmos o cadastro atual, perdemos o histórico do que estava impresso na NF-e
   - Cada NF-e referencia o snapshot (1:1), não o cadastro de pessoa

2. **Tabelas principais**
   - NFE_CABECALHO: ide + chave (44 chars), relacionamento com snapshots
   - NFE_ITEM: itens da nota (det), com ID_NFE referenciando NFE_CABECALHO
   - NFE_TOTAL: totalizadores (ICMSTot)
   - NFE_TRANSPORTE, NFE_FATURA, NFE_PARCELA, NFE_PAGAMENTO, NFE_INF_ADIC conforme o schema

3. **Tipos de dados**
   - Use tipos adequados: VARCHAR com tamanho correto, DECIMAL(15,2/4) para valores, TIMESTAMP para datas, SMALLINT/INTEGER para códigos
   - Evite palavras reservadas (ex: MOD → MOD_)

4. **Convenções**
   - Nomes em UPPER_SNAKE_CASE
   - Chave primária ID em todas as tabelas
   - Foreign keys com nomes descritivos (FK_NFE_ITEM, etc.)

Siga as convenções do projeto @delphi-nomenclatura.mdc
```

---

## PROMPT 3 — Unit Delphi de Importação

```
Crie uma unit Delphi para importar XML de NF-e e popular as tabelas do banco.

**Requisitos:**

1. **Tecnologia**
   - Use TXMLDocument (ou IXMLDocument) para ler o XML
   - Use FireDAC (TFDConnection, TFDQuery) para inserir no banco
   - Namespace: http://www.portalfiscal.inf.br/nfe

2. **Fluxo**
   - Receber caminho do arquivo XML
   - Validar se é NF-e (tag nfeProc ou NFe)
   - Extrair chave da NF-e e verificar se já existe (evitar duplicata)
   - Inserir na ordem: NFE_CABECALHO → NFE_EMITENTE_SNAPSHOT → NFE_DESTINATARIO_SNAPSHOT → NFE_ITEM → NFE_TOTAL → demais tabelas

3. **Tratamento**
   - Campos opcionais: verificar se a tag existe antes de ler
   - Valores numéricos: usar TryStrToFloat, StrToIntDef onde apropriado
   - Datas: converter formato ISO (YYYY-MM-DDTHH:nn:ss) para TDateTime
   - Transação: envolver todas as inserções em uma transação (rollback em caso de erro)

4. **Estrutura sugerida**
   - Classe TImportadorNFe ou procedures em unit uImportadorNFe
   - Parâmetros: AConnection (TFDConnection), ACaminhoXML (string)
   - Retorno: boolean (sucesso) ou raise exception com mensagem clara

5. **Convenções**
   - Siga @delphi-nomenclatura.mdc (T para classes, prefixos descritivos)
   - Tratamento de erros com mensagens em português
```

---

## PROMPT 4 — Formulários de Cadastro e Consulta

```
Com base nas tabelas NFE_CABECALHO, NFE_EMITENTE_SNAPSHOT, NFE_DESTINATARIO_SNAPSHOT e NFE_ITEM criadas, gere o código Delphi para:

1. **Formulário de consulta de NF-e** (TfrmConsultaNFe)
   - Filtros: período (data emissão), chave, número, emitente/destinatário
   - DBGrid com colunas principais: Chave, Número, Série, Data Emissão, Emitente, Destinatário, Valor Total
   - Botão para abrir detalhes da NF-e selecionada

2. **Formulário de detalhes da NF-e** (TfrmDetalheNFe)
   - Abas (PageControl): Cabeçalho | Emitente | Destinatário | Itens | Totais
   - Somente leitura (consulta)
   - Receber ID_NFE como parâmetro no Create

3. **Formulário de importação** (TfrmImportarNFe)
   - Campo para selecionar pasta com XMLs ou arquivo único
   - Botão Importar que chama a unit de importação
   - Lista/Log com resultado (sucesso, erro, duplicata)
   - ProgressBar ou indicador durante a importação

Use componentes padrão: DBGrid, DBEdit, DBNavigator, TDataSource, TFDQuery.
Siga @delphi-formularios.mdc e @delphi-cadastro-base.mdc.
Para cadastros simples, herdar de TfrmCadastroBase quando aplicável.
```

---

## PROMPT 5 — Prompt Unificado (Início do Projeto)

```
Preciso criar um sistema Delphi para gestão de XML de NF-e. O objetivo é importar XMLs de Notas Fiscais Eletrônicas, armazenar em banco de dados e permitir consulta.

**Stack:** Delphi [XE10 / 11 / 12], FireDAC, [Firebird / PostgreSQL / SQL Server]

**Entregas esperadas (em etapas):**

**Etapa 1 — Banco de dados**
- Analise o schema da NF-e v4 (leiauteNFe_v4.00.xsd do ACBr ou um XML de exemplo)
- Gere os scripts DDL com as tabelas necessárias
- OBRIGATÓRIO: use tabelas de snapshot (NFE_EMITENTE_SNAPSHOT, NFE_DESTINATARIO_SNAPSHOT) para emitente e destinatário, pois os dados devem ser preservados no momento da emissão (cadastros podem mudar depois)

**Etapa 2 — Importação**
- Unit Delphi que leia o XML com TXMLDocument e popule as tabelas via FireDAC
- Tratamento de duplicatas (chave já existe)
- Transação para garantir integridade
- Tratamento de campos opcionais e conversão de tipos

**Etapa 3 — Interface**
- Formulário de importação (selecionar pasta/arquivo, executar, ver log)
- Formulário de consulta com filtros
- Formulário de detalhes da NF-e (cabeçalho, emitente, destinatário, itens, totais)

**Convenções do projeto:**
- Consulte @delphi-nomenclatura.mdc, @delphi-formularios.mdc, @delphi-cadastro-base.mdc
- Nomenclatura: Tfrm para formulários, Tdm para DataModules, btn/ed/lbl para controles

**Referência técnica:** roteiro/07-projeto-xml-nfe-schema-tabelas.md
```

---

## Dicas de Uso

| Situação | O que fazer |
|----------|-------------|
| Primeira vez | Use o **PROMPT 5** (unificado) e peça para executar etapa por etapa |
| Já tem as tabelas | Use o **PROMPT 3** para a unit de importação |
| Quer ajustar o DDL | Use o **PROMPT 2** e especifique o SGBD |
| Só precisa dos forms | Use o **PROMPT 4** |
| XML diferente/atualizado | Use o **PROMPT 1** com o XML anexado |

---

## Arquivos de Referência no Projeto

- `roteiro/07-projeto-xml-nfe.md` — Visão geral do bloco
- `roteiro/07-projeto-xml-nfe-schema-tabelas.md` — Schema detalhado, DDL sugerido, estratégia de snapshots
- `.cursor/rules/delphi-*.mdc` — Convenções de código
