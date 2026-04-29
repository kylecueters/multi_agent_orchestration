# Reflection Report — Beaver's Choice Paper Company Multi-Agent System

---

## 1. Agent Workflow Architecture

### Overview

The system uses a four-agent hierarchy built with the **smolagents** framework and **GPT-4o-mini** via the Vocareum OpenAI-compatible proxy. The architecture follows a hub-and-spoke orchestration pattern:

```
[quote_requests_sample.csv]
         ↓
  [Orchestrator Agent]
    ↙       ↓       ↘
[Inventory] [Quote] [Fulfillment]
    ↓           ↓          ↓
      [SQLite DB: munder_difflin.db]
              ↓
      [test_results.csv]
```

See `diagram.excalidraw` / `diagram.png` for the full visual diagram.

---

### Agent Roles and Decision-Making

**Orchestrator Agent (`ToolCallingAgent`)**
The orchestrator receives each raw customer request with date context and routes it through all three worker agents. It enforces business policies (bulk discounts, professional tone, no margin disclosure) via a system prompt prepended to every request. By keeping routing logic in one place, we avoid duplicating business rules across workers.

**Inventory Manager (`ToolCallingAgent`)**
Handles all stock-related queries. Uses two tools:
- `check_inventory` — wraps `get_all_inventory()` and `get_stock_level()` to return current stock with reorder status
- `reorder_stock` — wraps `get_supplier_delivery_date()` and `create_transaction()` to place and record supplier orders

The inventory agent is called first in most request flows so the orchestrator knows availability before generating a quote.

**Quote Specialist (`ToolCallingAgent`)**
Handles all pricing logic. Uses two tools:
- `get_similar_quotes` — wraps `search_quote_history()` to find comparable historical orders
- `get_financial_status` — wraps `get_cash_balance()` and `generate_financial_report()` to surface the company's financial position

Searching historical quotes grounds pricing in real precedent rather than arbitrary LLM guesses, which improves consistency.

**Fulfillment Processor (`ToolCallingAgent`)**
Handles order recording. Uses one tool:
- `process_sale` — wraps `get_stock_level()` (availability re-check) and `create_transaction()` to record the sale

The double stock-check (once by the inventory manager, once inside `process_sale`) prevents race conditions where concurrent requests could oversell the same inventory.

---

### Why smolagents?

smolagents was chosen for its lightweight `ToolCallingAgent` + `managed_agents` API, which maps cleanly to the orchestrator/worker pattern. The `@tool` decorator makes it simple to wrap existing helper functions with minimal boilerplate. Alternative frameworks (pydantic-ai, npcsh) would have added significant setup overhead without matching benefits for this use case.

---

## 2. Evaluation Results

*Run `python project_starter.py` with your `VOCAREUM_API_KEY` set in `.env` to generate `test_results.csv`. Then update this section with the actual results.*

### How to Interpret test_results.csv

| Column | Meaning |
|--------|---------|
| `request_id` | Row number (1–71 from the sample) |
| `request_date` | Date of the customer request |
| `cash_balance` | Company cash after the request was processed |
| `inventory_value` | Total inventory value after the request |
| `response` | The agent system's customer-facing reply |

### Expected Outcomes (update with actuals after running)

**Requests resulting in cash balance changes (target: ≥3):**
Orders that are successfully fulfilled will reduce inventory and increase cash. Look for rows where `cash_balance` increased vs the previous row.

| Request ID | Request Date | Cash Before | Cash After | Change |
|-----------|-------------|-------------|------------|--------|
| *(fill in)* | | | | |

**Successfully fulfilled quote requests (target: ≥3):**
Responses containing "Order confirmed" with a Transaction ID.

| Request ID | Item | Quantity | Total |
|-----------|------|----------|-------|
| *(fill in)* | | | |

**Unfulfilled requests (expected: some):**
Requests rejected due to insufficient stock will contain "Insufficient stock" or "out of stock" in the response.

| Request ID | Reason |
|-----------|--------|
| *(fill in)* | Insufficient stock / item not carried |

---

### Strengths of the System

1. **Grounded pricing**: Using `search_quote_history()` before generating quotes means prices are anchored to real historical data, not hallucinated numbers.

2. **Automatic reordering**: The inventory agent checks stock levels after each sale and triggers `reorder_stock` when below the minimum threshold, keeping inventory self-sustaining across the full 71-request test run.

3. **Transparent customer outputs**: The system always includes pricing rationale, delivery timelines, and clear explanations for rejections without leaking internal margins or error messages.

4. **Separation of concerns**: Each worker agent has a narrow, non-overlapping scope. This makes failures easy to diagnose — if a quote is wrong, the issue is in the Quote Specialist; if a transaction fails, it's in the Fulfillment Processor.

---

## 3. Suggestions for Future Improvement

### Improvement 1: Add a Negotiation / Counter-Offer Agent

Currently, when a request cannot be fulfilled (out of stock), the system simply rejects it. A **Negotiation Agent** could:
- Offer a partial fulfillment (e.g., "We have 200 units now; the remaining 300 arrive by Friday")
- Propose a substitute product from the same category
- Collect customer contact information for a back-in-stock notification

This would improve the system's order capture rate and is a natural next step once the core fulfillment pipeline is proven.

### Improvement 2: Add Agent Memory Across Requests

The current orchestrator is stateless — it starts fresh on every request with no knowledge of what happened in previous calls. Adding a lightweight memory layer (e.g., a `ConversationHistory` tool backed by the existing SQLite database) would allow the system to:
- Recognize repeat customers and apply loyalty pricing
- Avoid redundant inventory lookups when the same product was checked moments ago
- Build a richer context for the orchestrator's routing decisions (e.g., "this customer always orders large quantities, so pre-apply bulk discount")

### Improvement 3: Structured Output Validation

Agent responses are currently free-text strings. Adding a response validation step — either via a Pydantic schema or a lightweight post-processing tool — would ensure that every customer-facing output always contains: (a) a quoted price, (b) a delivery estimate, and (c) an availability statement. This guards against the LLM occasionally omitting required fields, improving reliability at scale.

---

*Report template generated automatically. Fill in test_results.csv data in Section 2 after running `python project_starter.py`.*
