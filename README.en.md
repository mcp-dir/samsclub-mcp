# Sam's Club MCP

### Sam's Club in Claude, ChatGPT and AI agents via Open Finance

Connect your **Sam's Club** account to Claude, ChatGPT and AI agents via Brazil's Open Finance. Ask about Sam's Club balances, statements, credit-card bills and investments in natural language. Regulated by the Central Bank, read-only.

- 🏦 **Sam's Club via Brazil's Open Finance**, regulated by the Central Bank
- 💳 **Balances, statements, credit-card bills, investments and loans**
- 🔒 **Read-only** — the AI cannot move money
- 🔑 **Magic-link login**, explicit and revocable consent (LGPD)
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/customize/connectors?modal=add-custom-connector&mcpName=Sam's%20Club%20MCP&mcpServerUrl=https%3A%2F%2Fapi.mcp.ai%2Fp_samsclub)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors) → **+** → **Add custom connector** → name `Sam's Club MCP`, URL `https://api.mcp.ai/p_samsclub`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=samsclub&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9zYW1zY2x1YiJ9)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=samsclub&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_samsclub%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_samsclub
```

---

## 18 tools

| Tool | Description |
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

---

## Pricing

See [docs/precos.md](docs/precos.md) (PT-BR).

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_samsclub` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
