# BLOCO 4 — MCP: O Superpoder do Cursor (6–8 min)

[← Bloco 3 — Instalação](03-instalacao-configuracao.md) | **[Índice](../README.md)** | [Próximo: Bloco 5 — Skills e Prompts →](05-skills-prompts-delphi.md)

---

**Objetivo:** Explicar MCP de forma prática, sem teoria demais

---

### O que é MCP (em uma frase)

> *"É como dar 'ferramentas extras' para a IA — ela deixa de só falar e começa a agir"*

- **Exemplos do que o MCP permite:** ler/escrever arquivos, executar comandos no terminal, **acessar banco de dados**, buscar na web, etc.
- No curso usamos um MCP real: **MySQL** — a IA passa a poder consultar o banco (listar bancos/tabelas, ver esquema, executar SELECT).
- O MCP usa o **cliente MySQL** para Node.js (`mysql2`) para falar com o servidor MySQL/MariaDB.

---

### Exemplo real completo: MCP MySQL

Este repositório já traz um exemplo pronto em [`.cursor/mcp.json`](../.cursor/mcp.json).

**Pré-requisitos:** ter **Node.js** (já traz o `npx`), **MySQL** ou **MariaDB** instalado e um banco criado (ex.: `cursor_demo`).

---

### E quem não tem npx?

O `npx` vem junto com o **Node.js**. Quem não tem:

1. **Instalar o Node.js** (recomendado para este curso):
   - Acesse [nodejs.org](https://nodejs.org) e baixe a versão **LTS**.
   - Instale no Windows (Next até concluir). Marque a opção de adicionar ao PATH se aparecer.
   - Abra um **novo** terminal (PowerShell ou CMD) e teste: `npx --version`. Se aparecer um número, está pronto.
2. **Sem instalar Node.js:** o MCP de MySQL que usamos aqui **depende de Node/npx**. Nesse caso você pode:
   - Pular a parte de MCP de banco na prática e acompanhar só a explicação; ou
   - Usar outro MCP que não exija Node (por exemplo, alguns MCPs rodam via Docker ou executável — ver documentação de cada um).

**Resumo:** para rodar o exemplo deste bloco, instale o Node.js; o `npx` já vem incluso.

---

**1. Onde fica o arquivo**

- No **projeto:** `.cursor/mcp.json` (na raiz do repositório).
- A conexão é feita por **variáveis de ambiente** (`env`), então a senha não precisa ficar na connection string no Git.

**2. Conteúdo do arquivo (exemplo que está no projeto)**

```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": ["-y", "mysql-mcp-server"],
      "env": {
        "MYSQL_HOST": "localhost",
        "MYSQL_PORT": "3306",
        "MYSQL_USER": "root",
        "MYSQL_PASSWORD": "sua_senha_aqui",
        "MYSQL_DATABASE": "cursor_demo"
      }
    }
  }
}
```

- **O que isso faz:** sobe o servidor MCP **mysql-mcp-server** com `npx` e conecta no MySQL usando o cliente **mysql2** (driver oficial para Node.js).
- **Variáveis de ambiente:** `MYSQL_HOST`, `MYSQL_PORT`, `MYSQL_USER`, `MYSQL_PASSWORD`, `MYSQL_DATABASE` — ajuste com seus dados. Para não commitar a senha, use um arquivo local (ex.: copiar para `.cursor/mcp.local.json` e não versionar) ou preencher só na sua máquina.
- **Somente leitura:** esse MCP aceita apenas SELECT, SHOW, DESCRIBE e EXPLAIN (seguro para uso com a IA).

**Ferramentas disponíveis no MCP:**

| Ferramenta | Descrição |
|------------|-----------|
| `list_databases` | Lista os bancos acessíveis no servidor MySQL |
| `list_tables` | Lista as tabelas de um banco |
| `describe_table` | Mostra o esquema (colunas e tipos) de uma tabela |
| `execute_query` | Executa uma query SQL read-only (SELECT, SHOW, etc.) |

**3. Reiniciar o Cursor**

- Feche o Cursor **por completo** e abra de novo (alterações no `mcp.json` só valem após reiniciar).

**4. Conferir se o MCP está ativo**

- **Cursor Settings** (Ctrl+,) → **Features** ou **Tools & MCP** → conferir se o servidor `mysql` aparece e está ligado.

---

### Testar o MCP no chat (prática)

Com o MCP ativo, abra o **Chat** (ou Composer) e teste com prompts como:

| Objetivo | Prompt para colar no chat |
|----------|---------------------------|
| Listar bancos | *"Liste os bancos de dados disponíveis no MySQL usando o MCP."* |
| Listar tabelas | *"Quais tabelas existem no banco cursor_demo? Use as ferramentas do MCP."* |
| Ver esquema | *"Descreva o esquema da tabela X (colunas e tipos) usando o MCP de MySQL."* |
| Consultar dados | *"Execute um SELECT em uma tabela do banco e me mostre o resultado."* |

- A IA deve usar as **ferramentas** do MCP (`list_databases`, `list_tables`, `describe_table`, `execute_query`) e mostrar o resultado.
- Se não conectar: confira MySQL rodando, usuário/senha em `env`, Cursor reiniciado e MCP ligado nas Settings.

---

### Alternativa: PostgreSQL ou SQLite

Se quiser usar **PostgreSQL**, troque pelo MCP oficial:

```json
"postgres": {
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://usuario:senha@localhost:5432/banco"]
}
```

Para **SQLite** (arquivo `.db`, sem servidor):

```json
"sqlite": {
  "command": "npx",
  "args": ["-y", "mcp-sqlite", "C:\\caminho\\para\\arquivo.db"]
}
```

---

### Resumo para a gravação

1. Explicar MCP em uma frase (ferramentas extras para a IA).
2. Mostrar o arquivo `.cursor/mcp.json` do projeto com o exemplo **MySQL** e o uso do cliente (mysql2 via variáveis de ambiente).
3. Explicar as variáveis `env` (host, porta, usuário, senha, banco) e as ferramentas (list_databases, list_tables, describe_table, execute_query).
4. Reiniciar o Cursor e checar Settings → MCP.
5. No chat, pedir para listar bancos/tabelas ou rodar um SELECT e mostrar o resultado.

---

[← Bloco 3 — Instalação](03-instalacao-configuracao.md) | **[Índice](../README.md)** | [Próximo: Bloco 5 — Skills e Prompts →](05-skills-prompts-delphi.md)
