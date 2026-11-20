# Ferramentas

Conector MCP.AI para Sam's Club expõe 19 ferramentas (todas somente leitura).

### 1. `openfinance_search_bank_connectors`
**Input**: `keywords` (opcional), `include_accounts` (opcional)

Searches the available bank connectors by name (pass keywords[], e.g.

### 2. `openfinance_list_connections`
**Input**: nenhum input

Returns the saved bank connections for this install: connector_id, item_id, bank name, a per-connection reconnect_url, and an add_connection_url to link additional banks via the Open Finance widget.

### 3. `openfinance_get_item_status`
**Input**: `item` (opcional), `item_id` (opcional), `item_ids` (opcional)

Returns the current status of a bank connection (UPDATED, UPDATING, LOGIN_ERROR, etc.), its executionStatus, connector metadata, and a reconnect_url that reopens the widget in UPDATE mode for that connection (re-authe…

### 4. `openfinance_provider_status`
**Input**: nenhum input

Checks the LIVE operational status of the Open Finance provider (its public status page) — this is the PROVIDER's health, separate from your own connection's `openfinance_get_item_status`.

### 5. `openfinance_list_accounts`
**Input**: `item` (opcional), `item_id` (opcional), `type` (opcional), `item_ids` (opcional)

Returns accounts for a bank connection: BANK (checking/savings) and CREDIT (credit card) with balance, number, type, subtype, bankData, and creditData.

### 6. `openfinance_list_transactions`
**Input**: `account_id`, `from` (opcional), `to` (opcional), `page` (opcional), `page_size` (opcional), `search_queries` (opcional), `detail` (opcional), `account_ids` (opcional)

Returns transactions for a bank account (BANK or CREDIT type).

### 7. `openfinance_list_transactions_by_item`
**Input**: `item` (opcional), `item_id` (opcional), `from` (opcional), `to` (opcional), `type` (opcional), `granularity` (opcional), `top_n` (opcional), `detail` (opcional), `item_ids` (opcional)

Consolidated cash-flow analysis for a whole bank CONNECTION over a period, in ONE call.

### 8. `openfinance_list_credit_card_bills`
**Input**: `account_id`, `page` (opcional), `page_size` (opcional), `include_open_bill` (opcional), `account_ids` (opcional)

Returns CLOSED credit card bills for a CREDIT-type account: dueDate, totalAmount, minimumPaymentAmount, allowsInstallments, plus `payments[]` (id, paymentDate, amount, valueType, paymentMode), `payments_count`, `payme…

### 9. `openfinance_list_investments`
**Input**: `item` (opcional), `item_id` (opcional), `type` (opcional), `page` (opcional), `page_size` (opcional), `item_ids` (opcional)

Returns the investment portfolio for a connection (broker or bank with INVESTMENTS product enabled): FIIs, stocks, ETFs, fixed income (CDB/LCI/LCA/Tesouro), mutual funds, retirement (previdência) and COE.

### 10. `openfinance_list_investment_transactions`
**Input**: `investment_id`, `page` (opcional), `page_size` (opcional), `investment_ids` (opcional)

Returns the movement history for a specific investment position: BUY / SELL / TAX / INTEREST / AMORTIZATION / TRANSFER.

### 11. `openfinance_list_loans`
**Input**: `items` (opcional)

Lists loan contracts per bank connection (GET /loans).

### 12. `openfinance_get_loan_detail`
**Input**: `loan_ids`

Returns full loan contract detail by id (GET /loans/:loanId): interestRates[] (taxType, ratePercentage, indexer), contractedFinanceCharges[], balloonPayments[], warranties[], installments schedule (installmentsCount,…

### 13. `openfinance_force_sync`
**Input**: `items` (opcional), `wait` (opcional)

Forces the bank to re-sync one or more connections NOW and WAITS for it to finish (PATCH /items/:id, then polls until the item stops updating, up to ~60s).

### 14. `openfinance_get_account_balance`
**Input**: `account_ids`

Returns the latest available balance per account id (GET /accounts/:id/balance).

### 15. `openfinance_get_accounts_detail`
**Input**: `account_ids`

Returns full account objects including extended creditData (additional cards, limits) per id (GET /accounts/:id).

### 16. `openfinance_get_credit_card_bill`
**Input**: `bill_ids`, `include_transactions` (opcional), `account_id` (opcional), `transactions_detail` (opcional)

Returns bill-level detail for one or more credit card bills by id (GET /bills/:id): `dueDate`, `billClosingDate` (when the cycle closed — the boundary that defines which purchases belong to this bill), `totalAmount`,…

### 17. `openfinance_list_categories`
**Input**: nenhum input

Returns the provider's transaction category taxonomy (GET /categories), cached for the adapter session.

### 18. `openfinance_update_transaction_category`
**Input**: `items`

Corrects the category of one or more transactions (PATCH /transactions/:id).

### 19. `openfinance_disconnect_bank`
**Input**: `item`

Revokes the Open Finance consent for a specific bank and deletes the connection data.

## Prompts de exemplo

```
Quanto gastei no cartão do Sam's Club esse mês?
Resuma minha fatura do Sam's Club em aberto
Qual meu saldo na conta do Sam's Club?
Como está minha carteira de investimentos no Sam's Club?
```
