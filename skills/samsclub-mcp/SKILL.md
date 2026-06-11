---
name: samsclub-mcp
description: Dados bancários do Sam's Club via Open Finance Brasil: saldos, extratos, faturas de cartão, investimentos e empréstimos. Use quando o usuário perguntar sobre dinheiro/conta/cartão/investimentos do Sam's Club.
---

# Sam's Club MCP — REST API skill

Você tem acesso à **Sam's Club MCP** REST API na MCP.AI.

> Conecte sua conta do **Sam's Club** ao Claude, ChatGPT e agentes de IA via Open Finance Brasil. Pergunte sobre saldos, extratos, faturas de cartão e investimentos do Sam's Club em linguagem natural. Regulado pelo Banco Central, somente leitura.

## Base URL

```
https://api.mcp.ai/api/openfinance
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/openfinance/connectors/search \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"keywords":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/openfinance/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (16)

#### `openfinance_search_bank_connectors`

Buscar conectores de banco (Open Finance/API) por nome _(POST /api/openfinance/connectors/search)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `keywords` | string[] | Sim | Termos do nome/id do banco (match OR), ex.: ['nubank','btg']. Obrigatório. |
| `include_accounts` | boolean | Não | Inclui contas (e contagem) de cada conexão já ligada. Custa 1 chamada por conexão; default false. |

#### `openfinance_list_connections`

Listar bancos conectados _(POST /api/openfinance/connections/list)_

#### `openfinance_get_item_status`

Status de uma conexão (UPDATED, LOGIN_ERROR…) _(POST /api/openfinance/connections/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `item` | string | Não | item_id (uuid), connector_id ('612') ou connector_name ('Nubank'). Omita se há só 1 conexão. |

#### `openfinance_force_sync`

Forçar sincronização de uma ou mais conexões _(POST /api/openfinance/connections/sync)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `items` | string[] | Sim | Seletores das conexões (item_id, connector_id ou connector_name). 1-50. |

#### `openfinance_disconnect_bank`

Revogar consentimento Open Finance de um banco _(POST /api/openfinance/connections/disconnect)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `item` | string | Sim | item_id (uuid), connector_id ou connector_name da conexão. |

#### `openfinance_list_accounts`

Listar contas (BANK / CREDIT) de uma conexão _(POST /api/openfinance/accounts/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `item` | string | Não | Conexão alvo (item_id / connector_id / connector_name). |
| `type` | string | Não | Filtrar por tipo. (BANK, CREDIT) |

#### `openfinance_get_accounts_detail`

Detalhe completo de contas por id (batch 1-50) _(POST /api/openfinance/accounts/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account_ids` | string[] | Sim | uuids das contas. 1-50. |

#### `openfinance_get_account_balance`

Saldo em tempo real por conta (batch 1-50) _(POST /api/openfinance/accounts/balance)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account_ids` | string[] | Sim | uuids das contas. 1-50. |

#### `openfinance_list_transactions`

Transações por conta (BANK ou CREDIT) com filtros de data/keyword _(POST /api/openfinance/transactions/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account_id` | string | Sim | uuid da conta. |
| `from` | string | Não | Data início ISO (YYYY-MM-DD). |
| `to` | string | Não | Data fim ISO (YYYY-MM-DD). |
| `page` | number | Não | Página (default 1). |
| `page_size` | number | Não | Itens por página (1-500, default 50). |
| `search_queries` | string[] | Não | Filtro keyword (OR). Triggera scan agregado em from/to. |

#### `openfinance_list_credit_card_bills`

Faturas de cartão (com payment_status derivado) _(POST /api/openfinance/credit-card-bills/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account_id` | string | Sim | uuid de conta CREDIT. |
| `page` | number | Não |  |
| `page_size` | number | Não | 1-100. |

#### `openfinance_get_credit_card_bill`

Detalhe de fatura por id (batch 1-50) _(POST /api/openfinance/credit-card-bills/detail)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `bill_ids` | string[] | Sim | uuids das faturas. 1-50. |

#### `openfinance_list_investments`

Carteira de investimentos por conexão _(POST /api/openfinance/investments/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `item` | string | Não |  |
| `type` | string | Não | Filtrar por tipo. (COE, EQUITY, ETF, FIXED_INCOME, MUTUAL_FUND, SECURITY, OTHER) |
| `page` | number | Não |  |
| `page_size` | number | Não | 1-500, default 100. |

#### `openfinance_list_investment_transactions`

Movimentação de uma posição de investimento (BUY/SELL/TAX/…) _(POST /api/openfinance/investments/transactions/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `investment_id` | string | Sim | uuid do investment. |
| `page` | number | Não |  |
| `page_size` | number | Não | 1-500, default 100. |

#### `openfinance_list_loans`

Contratos de empréstimo por conexão (batch) _(POST /api/openfinance/loans/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `items` | string[] | Sim | Seletores das conexões. 1-50. |

#### `openfinance_list_categories`

Taxonomia de categorias de transação (the provider) _(POST /api/openfinance/categories/list)_

#### `openfinance_update_transaction_category`

Corrigir categoria de transações (cria regra automática) _(POST /api/openfinance/transactions/category)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `items` | object[] | Sim | Pares { transaction_id, category_id }. 1-50. category_id vem de /categories/list. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_samsclub` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
