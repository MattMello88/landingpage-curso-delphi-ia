# BLOCO 5 — Rules e Guidelines (4–5 min)

[← Bloco 4 — MCP](04-mcp.md) | **[Índice](../README.md)** | [Próximo: Bloco 6 — Skills e Prompts →](06-skills-prompts-delphi.md)

---

**Objetivo:** Mostrar como configurar Rules e Guidelines no Cursor para manter consistência e qualidade do código

- O que são Rules e Guidelines no Cursor
- Diferença entre Rules globais e Rules de projeto
- Onde ficam: `.cursor/rules/`, `AGENTS.md`, `RULE.md`
- Como a IA usa as rules automaticamente em cada conversa

---

### Exemplos práticos para Delphi (Rules que você pode colocar no projeto)

#### 1. Padrão de nomenclatura

| Elemento | Padrão | Exemplo |
|----------|--------|---------|
| Formulários | `Tfrm` + nome descritivo | `TfrmCliente`, `TfrmProduto` |
| DataModules | `Tdm` + nome | `TdmPrincipal`, `TdmVendas` |
| Units | prefixo do tipo + nome | `uFrmCliente`, `uDmPrincipal` |
| Classes de negócio | `T` + nome singular | `TCliente`, `TPedido` |
| Botões | `btn` + ação | `btnSalvar`, `btnCancelar` |
| Edits | `ed` + nome do campo | `edNome`, `edEmail` |
| Labels | `lbl` + nome | `lblNome`, `lblCodigo` |
| Queries/Datasets | `qry` / `ds` + nome | `qryCliente`, `dsCliente` |

**Exemplo de Rule:** *"No Delphi, use Tfrm para formulários, Tdm para DataModules, prefixos btn/ed/lbl para controles e qry/ds para queries e datasources."*

---

#### 2. Boas práticas de uso da classe (formulário)

- **Criar/abrir:** usar `Create(Application)` e `Show` ou `ShowModal`; não reutilizar instância solta.
- **Liberar:** quem criou com `Create` deve chamar `Free` (ou usar `try/finally`); em `ShowModal`, dar `Free` após o `ShowModal` retornar.
- **Passar dados:** preferir parâmetros no `Create` ou propriedades antes do `Show`, em vez de variáveis globais.
- **Evitar:** `Application.CreateForm` para forms que não são a tela principal; preferir criação sob demanda.

**Exemplo de Rule:** *"Formulários Delphi: criar com Create(Application), usar ShowModal para telas modais e garantir Free após uso. Evitar Application.CreateForm para telas secundárias."*

---

#### 3. Ancestrais para cadastros simples

- **Objetivo:** um formulário base (ancestral) com toolbar (Incluir, Editar, Excluir, Gravar, Cancelar), grid, navegação e regras comuns.
- **Nome sugerido:** `TfrmCadastroBase` (unit `uFrmCadastroBase`).
- **O que o ancestral já traz:** botões de ação, `DataSource` + `DBGrid`, tratamento de modo (Inserção/Edição), `Abort` na validação.
- **Cadastro simples (ex.: Cadastro de Cidade):** herdar de `TfrmCadastroBase`, definir `Caption`, conectar `TQuery`/`TTable` ao `DataSource`, e opcionalmente sobrescrever `ValidarAntesGravar` e `PosGravar`.

**Exemplo de Rule:** *"Para cadastros simples, herdar de TfrmCadastroBase; definir apenas Caption, Dataset e validações específicas. Não duplicar lógica de toolbar e navegação."*

---

#### 4. Cadastro pai e filho (mestre-detalhe)

- **Estrutura:** um formulário com dois grids (ou um grid mestre e um grid detalhe): ex. Cliente (pai) e Contatos do cliente (filho).
- **Ancestral sugerido:** `TfrmCadastroMestreDetalhe` herdando de `TfrmCadastroBase`, com dois `DataSource` (pai e filho), `MasterSource`/`MasterFields` no dataset filho e botões Incluir/Excluir no detalhe.
- **Uso:** o usuário navega no mestre; o grid do filho mostra só os registros ligados ao registro atual do mestre. Incluir/Excluir no detalhe só afetam o filho.
- **Nomenclatura:** datasets `qryMestre`/`qryDetalhe` ou `qryCliente`/`qryContato`; manter `MasterSource` e `MasterFields` configurados no filho.

**Exemplo de Rule:** *"Em cadastros pai e filho, usar TfrmCadastroMestreDetalhe; configurar MasterSource e MasterFields no dataset filho; manter dois DataSource e não permitir filho órfão (sem mestre selecionado)."*

---

#### 5. Uso do componente Excel (exportar/importar)

- **Objetivo:** exportar grid/dados para Excel ou ler planilha sem depender de OLE Automation pesado; usar componente de terceiros (ex.: FlexCel, TMS, ou biblioteca que encapsule Excel).
- **Boas práticas:**
  - Não deixar processo do Excel aberto em background: abrir, gerar/ler arquivo, fechar e liberar objeto.
  - Preferir gerar arquivo .xlsx em disco e abrir no Excel (ou apenas informar caminho ao usuário) em vez de controlar a aplicação Excel via OLE.
  - Em imports: validar colunas esperadas, tratar erros de célula vazia ou tipo e logar linhas com problema.
- **Exemplo de uso (exportar grid):** percorrer `DataSet` ou linhas do grid, escrever linha a linha na planilha; na primeira linha, escrever cabeçalhos (nomes dos campos ou do grid).
- **Exemplo de Rule:** *"Ao usar componente Excel: abrir conexão/arquivo, executar leitura ou gravação e fechar/liberar em seguida. Em exportação, primeira linha = cabeçalhos. Em importação, validar colunas e registrar linhas com erro."*

---

### Resumo para a gravação

1. Explicar Rules e Guidelines e onde ficam (`.cursor/rules/`, `AGENTS.md`).
2. Mostrar um exemplo de Rule de nomenclatura e um de boas práticas de classe.
3. Mostrar ancestral para cadastro simples (TfrmCadastroBase) e para pai e filho (TfrmCadastroMestreDetalhe).
4. Citar uso do componente Excel (abrir/fechar, exportar com cabeçalho, importar com validação).

---

[← Bloco 4 — MCP](04-mcp.md) | **[Índice](../README.md)** | [Próximo: Bloco 6 — Skills e Prompts →](06-skills-prompts-delphi.md)
