# BLOCO 4 — MCP - Model Context Protocol: O Superpoder do Cursor (6–8 min)

[← Bloco 3 — Instalação](03-instalacao-configuracao.md) | **[Índice](../README.md)** | [Próximo: Bloco 5 — Rules e Guidelines →](05-rules-guidelines.md)

---

**Objetivo:** Explicar MCP de forma prática, sem teoria demais

---

### O que é MCP (em uma frase)

> *"É como dar 'ferramentas extras' para a IA — ela deixa de só falar e começa a agir"*

- **Exemplos do que o MCP permite:** ler/escrever arquivos, executar comandos no terminal, acessar banco de dados, buscar na web, etc.
- Dois exemplos práticos que usamos aqui:
  1. **Filesystem** — a IA pode ler arquivos e documentação em pastas que você permite (ideal para docs, specs, código).
  2. **MySQL** — a IA passa a poder consultar o banco (listar bancos/tabelas, ver esquema, executar SELECT).

---

### Exemplo 1: MCP Filesystem (ler arquivos e documentação)

O MCP **Filesystem** permite que a IA leia e escreva arquivos em pastas que você liberar. É muito útil para:
- Ler a documentação do projeto
- Ler arquivos de configuração
- Acessar especificações, roteiros e notas

**Pré-requisito:** ter **Node.js** instalado (já traz o `npx`).

---

**1. Configurar o MCP Filesystem**

Edite o arquivo `.cursor/mcp.json` (na raiz do projeto) e adicione o servidor:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\Users\\seu_usuario\\source\\github\\seu_projeto",
        "C:\\caminho\\para\\documentacao"
      ]
    }
  }
}
```

- **O que faz:** cada caminho nos `args` é uma pasta permitida. A IA só pode ler/escrever dentro dessas pastas.
- **Windows:** use barras duplas `\\` ou barras normais `/`. Exemplo: `C:/Users/joao/projetos/curso-delphi`.
- **Dica:** inclua a raiz do seu projeto, pastas onde ficam docs/specs/manuais e a **pasta que será o ancestral dos formulários Delphi** (ex: `C:/Projetos/MeuProjetoDelphi` ou pasta Forms).

**2. Ferramentas disponíveis no MCP Filesystem**

| Ferramenta | Descrição |
|------------|-----------|
| `read_file` | Lê o conteúdo completo de um arquivo |
| `read_multiple_files` | Lê vários arquivos de uma vez (útil para comparar) |
| `list_directory` | Lista arquivos e pastas de um diretório |
| `directory_tree` | Mostra a árvore de arquivos em JSON |
| `search_files` | Busca arquivos por padrão (nome, extensão) |
| `get_file_info` | Informações do arquivo (tamanho, datas) |

**3. Reiniciar o Cursor**

- Feche o Cursor **por completo** e abra de novo (alterações no `mcp.json` só valem após reiniciar).

**4. Testar no chat**

Com o MCP ativo, abra o **Chat** (ou Composer) e teste:

| Objetivo | Prompt para colar no chat |
|----------|---------------------------|
| Ler documentação | *"Leia o conteúdo do arquivo README.md do projeto usando o MCP Filesystem."* |
| Listar pastas | *"Liste os arquivos da pasta roteiro usando o MCP."* |
| **Ler pasta ancestral dos formulários Delphi** | *"Liste os arquivos da pasta que será o ancestral dos formulários do Delphi (ex: pasta Forms ou do Projeto Delphi) usando o MCP."* |
| Buscar arquivos | *"Busque todos os arquivos .md no projeto."* |
| Ler roteiro | *"Leia o roteiro 03-instalacao-configuracao.md e me resuma o conteúdo."* |

- A IA usará `read_file`, `list_directory` ou `search_files` para acessar os arquivos que você permitiu.

---

### Exemplo 2: MCP MySQL (consultar banco de dados)

Se você tiver **MySQL** ou **MariaDB** instalado, pode adicionar o MCP MySQL no mesmo `mcp.json`:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\Users\\seu_usuario\\source\\github\\seu_projeto"
      ]
    },
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

**Ferramentas do MySQL:** `list_databases`, `list_tables`, `describe_table`, `execute_query` (somente leitura).

**Prompts de teste:** *"Liste os bancos de dados"*, *"Quais tabelas existem no banco cursor_demo?"*, *"Execute um SELECT em uma tabela."*

---

### E quem não tem npx?

O `npx` vem junto com o **Node.js**. Quem não tem:

1. **Instalar o Node.js** (recomendado para este curso):
   - Acesse [nodejs.org](https://nodejs.org) e baixe a versão **LTS**.
   - Instale no Windows (Next até concluir). Marque a opção de adicionar ao PATH se aparecer.
   - Abra um **novo** terminal e teste: `npx --version`. Se aparecer um número, está pronto.
2. **Sem Node.js:** o MCP Filesystem e o MySQL que usamos **dependem de Node/npx**. Você pode pular a prática e acompanhar só a explicação, ou usar outros MCPs que rodem via Docker/executável (ver documentação de cada um).

**Resumo:** para rodar os exemplos deste bloco, instale o Node.js; o `npx` já vem incluso.

---

### Conferir se o MCP está ativo

- **Cursor Settings** (Ctrl+,) → **Features** ou **Tools & MCP** → conferir se os servidores aparecem e estão ligados.

---

### Resumo para a gravação

1. Explicar MCP em uma frase (ferramentas extras para a IA).
2. Mostrar o MCP **Filesystem** primeiro: configurar no `mcp.json` com os caminhos das pastas permitidas, explicar `read_file` e `list_directory`.
3. Mostrar como usar no chat: pedir para ler um README, listar arquivos ou buscar documentação.
4. Opcional: mostrar o MCP MySQL para quem quer consultar banco.
5. Reiniciar o Cursor e checar Settings → MCP.

---

[← Bloco 3 — Instalação](03-instalacao-configuracao.md) | **[Índice](../README.md)** | [Próximo: Bloco 5 — Rules e Guidelines →](05-rules-guidelines.md)
