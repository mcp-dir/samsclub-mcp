# MCP.AI connector for Sam's Club (unofficial)

### Use your Sam's Club data in Claude, ChatGPT and AI agents via Open Finance

> ⚠️ MCP.AI is not affiliated with, sponsored or endorsed by Sam's Club. Sam's Club is a registered trademark of its owner and is mentioned only to indicate which institution this connector works with. Data access happens through Brazil's Open Finance, regulated by the Central Bank, with the customer's own authorization.

Connect your **Sam's Club** account to Claude, ChatGPT and AI agents via Brazil's Open Finance. Ask about Sam's Club balances, statements, credit-card bills and investments in natural language. Regulated by the Central Bank, read-only.

- 🏦 **Sam's Club via Brazil's Open Finance**, regulated by the Central Bank
- 💳 **Balances, statements, credit-card bills, investments and loans**
- 🔒 **Read-only** — the AI cannot move money
- 🔑 **Magic-link login**, explicit and revocable consent (LGPD)
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue

[Versão em português](README.md) · [Full docs (PT-BR)](docs/) · [Agent skill](skills/)

---

## One-click install

### Claude (Web and Desktop)

Anthropic unified MCP installation at `claude.ai/customize/connectors`. **The same link works for Claude Web and Claude Desktop** (just be logged in):

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (if the deeplink does not open): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → paste **Name** `Conector MCP.AI para Sam's Club` and **URL** `https://api.mcp.ai/p_samsclub`.

### Cursor

[➕ Install Conector MCP.AI para Sam's Club in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=samsclub&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9zYW1zY2x1YiJ9)

### VS Code (Copilot Chat)

[➕ Install Conector MCP.AI para Sam's Club in VS Code](vscode:mcp/install?name=samsclub&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_samsclub%22%7D)

### ChatGPT, Manus, OpenClaw and 40+ other clients

Works with any MCP client that speaks **MCP over HTTP**. The server URL is always:

```
https://api.mcp.ai/p_samsclub
```

Per-client details: [INSTALL.md](INSTALL.md).

---

## Example prompts

```
How much did I spend on my Sam's Club card this month?
Summarize my open Sam's Club credit-card bill
What's my Sam's Club account balance?
```

---

## 19 tools available

| Tool | Description |
|---|---|
| `openfinance_search_bank_connectors` | Searches the available bank connectors by name (pass keywords[], e.g. |
| `openfinance_list_connections` | Returns the saved bank connections for this install: connector_id, item_id, bank name, a per-connection reconnect_url, and an add_connection_url to link additional banks via the Open Finance widget. |
| `openfinance_get_item_status` | Returns the current status of a bank connection (UPDATED, UPDATING, LOGIN_ERROR, etc.), its executionStatus, connector metadata, and a reconnect_url that reopens the widget in UPDATE mode for that connection (re-authe… |
| `openfinance_provider_status` | Checks the LIVE operational status of the Open Finance provider (its public status page) — this is the PROVIDER's health, separate from your own connection's `openfinance_get_item_status`. |
| `openfinance_list_accounts` | Returns accounts for a bank connection: BANK (checking/savings) and CREDIT (credit card) with balance, number, type, subtype, bankData, and creditData. |
| `openfinance_list_transactions` | Returns transactions for a bank account (BANK or CREDIT type). |
| `openfinance_list_transactions_by_item` | Consolidated cash-flow analysis for a whole bank CONNECTION over a period, in ONE call. |
| `openfinance_list_credit_card_bills` | Returns CLOSED credit card bills for a CREDIT-type account: dueDate, totalAmount, minimumPaymentAmount, allowsInstallments, plus `payments[]` (id, paymentDate, amount, valueType, paymentMode), `payments_count`, `payme… |
| `openfinance_list_investments` | Returns the investment portfolio for a connection (broker or bank with INVESTMENTS product enabled): FIIs, stocks, ETFs, fixed income (CDB/LCI/LCA/Tesouro), mutual funds, retirement (previdência) and COE. |
| `openfinance_list_investment_transactions` | Returns the movement history for a specific investment position: BUY / SELL / TAX / INTEREST / AMORTIZATION / TRANSFER. |
| `openfinance_list_loans` | Lists loan contracts per bank connection (GET /loans). |
| `openfinance_get_loan_detail` | Returns full loan contract detail by id (GET /loans/:loanId): interestRates[] (taxType, ratePercentage, indexer), contractedFinanceCharges[], balloonPayments[], warranties[], installments schedule (installmentsCount,… |
| `openfinance_force_sync` | Forces the bank to re-sync one or more connections NOW and WAITS for it to finish (PATCH /items/:id, then polls until the item stops updating, up to ~60s). |
| `openfinance_get_account_balance` | Returns the latest available balance per account id (GET /accounts/:id/balance). |
| `openfinance_get_accounts_detail` | Returns full account objects including extended creditData (additional cards, limits) per id (GET /accounts/:id). |
| `openfinance_get_credit_card_bill` | Returns bill-level detail for one or more credit card bills by id (GET /bills/:id): `dueDate`, `billClosingDate` (when the cycle closed — the boundary that defines which purchases belong to this bill), `totalAmount`,… |
| `openfinance_list_categories` | Returns the provider's transaction category taxonomy (GET /categories), cached for the adapter session. |
| `openfinance_update_transaction_category` | Corrects the category of one or more transactions (PATCH /transactions/:id). |
| `openfinance_disconnect_bank` | Revokes the Open Finance consent for a specific bank and deletes the connection data. |

Details for each tool: [docs/ferramentas.md](docs/ferramentas.md) (PT-BR)

---

## Pricing

See [docs/precos.md](docs/precos.md) (PT-BR).

---

## Privacy & data protection

- **Read-only**, no tool changes data at the source.
- **Sub-processors**: the LLM host you choose (Claude, ChatGPT, Cursor, your own agent). Full list in [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Data returned by the tools is sent to **the LLM host you choose**, a sub-processor outside our control. We recommend plans with training opt-out.

---

## FAQ

**Is MCP.AI affiliated with Sam's Club?**
MCP.AI is not affiliated with, sponsored or endorsed by Sam's Club. Sam's Club is a registered trademark of its owner and is mentioned only to indicate which institution this connector works with. Data access happens through Brazil's Open Finance, regulated by the Central Bank, with the customer's own authorization.

**How does it work?**
Through Brazil's Open Finance (regulated by the Central Bank). You connect your Sam's Club account with explicit consent; the AI reads balances, statements, bills and investments. Read-only.

**Can the AI move money?**
No. 100% read-only, Open Finance does not allow payments through this path.

**Is the server open source?**
The server is proprietary (hosted). This repository is the public wrapper with manifests, docs and skills, all MIT.


---

## Support

- 📧 [samsclub@mcp.ai](mailto:samsclub@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/samsclub-mcp/issues)
- 📄 [docs/](docs/)

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_samsclub` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
