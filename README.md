# Sam's Club MCP

### Sam's Club no Claude, ChatGPT e agentes de IA via Open Finance

Conecte sua conta do **Sam's Club** ao Claude, ChatGPT e agentes de IA via Open Finance Brasil. Pergunte sobre saldos, extratos, faturas de cartão e investimentos do Sam's Club em linguagem natural. Regulado pelo Banco Central, somente leitura.

- 🏦 **Sam's Club via Open Finance Brasil**, regulado pelo Banco Central
- 💳 **Saldos, extratos, faturas de cartão, investimentos e empréstimos**
- 🔒 **Somente leitura** — a IA não movimenta dinheiro
- 🔑 **Login por magic-link**, consentimento explícito e revogável (LGPD)
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/customize/connectors?modal=add-custom-connector&mcpName=Sam's%20Club%20MCP&mcpServerUrl=https%3A%2F%2Fapi.mcp.ai%2Fp_samsclub)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors) → **+** → **Adicionar conector personalizado** → cole **Nome** `Sam's Club MCP` e **URL** `https://api.mcp.ai/p_samsclub`.

### Cursor

[➕ Instalar Sam's Club MCP no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=samsclub&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9zYW1zY2x1YiJ9)

### VS Code (Copilot Chat)

[➕ Instalar Sam's Club MCP no VS Code](vscode:mcp/install?name=samsclub&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_samsclub%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_samsclub
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Quanto gastei no cartão do Sam's Club esse mês?
Resuma minha fatura do Sam's Club em aberto
Qual meu saldo na conta do Sam's Club?
Como está minha carteira de investimentos no Sam's Club?
```

---

## 18 ferramentas disponíveis

| Tool | Descrição |
|---|---|
| `openfinance_search_bank_connectors` | Searches the available bank connectors by name (pass keywords[], e.g. |
| `openfinance_list_connections` | Returns the saved bank connections for this install: connector_id, item_id, bank name, and an add_connection_url to link additional banks via the Open Finance widget. |
| `openfinance_get_item_status` | Returns the current status of a bank connection (UPDATED, UPDATING, LOGIN_ERROR, etc.), its executionStatus, and connector metadata. |
| `openfinance_provider_status` | Checks the LIVE operational status of the Open Finance provider (its public status page) — this is the PROVIDER's health, separate from your own connection's `openfinance_get_item_status`. |
| `openfinance_list_accounts` | Returns accounts for a bank connection: BANK (checking/savings) and CREDIT (credit card) with balance, number, type, subtype, bankData, and creditData. |
| `openfinance_list_transactions` | Returns transactions for a bank account (BANK or CREDIT type). |
| `openfinance_list_transactions_by_item` | Consolidated cash-flow analysis for a whole bank CONNECTION over a period, in ONE call. |
| `openfinance_list_credit_card_bills` | Returns CLOSED credit card bills for a CREDIT-type account: dueDate, totalAmount, minimumPaymentAmount, allowsInstallments, plus `payments[]` (id, paymentDate, amount, valueType, paymentMode), `payments_count`, `payme… |
| `openfinance_list_investments` | Returns the investment portfolio for a connection (broker or bank with INVESTMENTS product enabled): FIIs, stocks, ETFs, fixed income (CDB/LCI/LCA/Tesouro), mutual funds, retirement (previdência) and COE. |
| `openfinance_list_investment_transactions` | Returns the movement history for a specific investment position: BUY / SELL / TAX / INTEREST / AMORTIZATION / TRANSFER. |
| `openfinance_list_loans` | Lists loan contracts per bank connection (GET /loans). |
| `openfinance_force_sync` | Forces the bank to re-sync one or more connections NOW and WAITS for it to finish (PATCH /items/:id, then polls until the item stops updating, up to ~60s). |
| `openfinance_get_account_balance` | Returns real-time balance payload per account id (GET /accounts/:id/balance). |
| `openfinance_get_accounts_detail` | Returns full account objects including extended creditData (additional cards, limits) per id (GET /accounts/:id). |
| `openfinance_get_credit_card_bill` | Returns bill-level detail for one or more credit card bills by id (GET /bills/:id): financeCharges and payments[] (id, paymentDate, amount, valueType, paymentMode). |
| `openfinance_list_categories` | Returns the provider's transaction category taxonomy (GET /categories), cached for the adapter session. |
| `openfinance_update_transaction_category` | Corrects the category of one or more transactions (PATCH /transactions/:id). |
| `openfinance_disconnect_bank` | Revokes the Open Finance consent for a specific bank and deletes the connection data. |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Somente leitura**, nenhuma ferramenta altera dados na origem.
- **Sub-processadores**: o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**Como funciona?**
Via Open Finance Brasil (regulado pelo Banco Central). Você conecta sua conta Sam's Club com consentimento explícito; a IA lê saldos, extratos, faturas e investimentos. Somente leitura.

**A IA pode movimentar dinheiro?**
Não. 100% leitura — Open Finance não permite movimentação por essa via.

**Só funciona com o Sam's Club?**
Este MCP é focado no Sam's Club. Para conectar vários bancos de uma vez, use o Banco MCP (api.mcp.ai/banco).

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills, tudo MIT.


---

## Suporte

- 📧 [samsclub@mcp.ai](mailto:samsclub@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/samsclub-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_samsclub` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
