# Merchant Domain Scam & Rug-Pull Guard MCP

Remote **Model Context Protocol (MCP)** server for autonomous shopping, procurement, and payment agents.

Before an AI agent spends a user's credit card or stablecoins on an unfamiliar e-commerce store or paid API domain, it can inspect schemas and scoring rubrics for **$0.00**, then call paid verification tools for **$0.005–$0.01 USDC on Base (`eip155:8453`)** via **x402 (PayAI Facilitator)** to receive a deterministic `0–100` risk score, `ALLOW` / `CAUTION` / `BLOCK` verdict, machine-readable `block_reasons`, and live threat-intelligence evidence.

> **Hosted Remote Server (Streamable HTTP):** `https://merchant-scam-guard-mcp.vercel.app/mcp`

---

## Quick Connect

### Generic MCP Client / Cursor / Windsurf

```json
{
  "mcpServers": {
    "merchant-scam-guard": {
      "url": "https://merchant-scam-guard-mcp.vercel.app/mcp"
    }
  }
}
```

### VS Code (`.vscode/mcp.json`)

```json
{
  "servers": {
    "merchant-scam-guard": {
      "type": "http",
      "url": "https://merchant-scam-guard-mcp.vercel.app/mcp"
    }
  }
}
```

---

## Endpoints

| Route | Method(s) | Billing | Description |
| :--- | :--- | :--- | :--- |
| `https://merchant-scam-guard-mcp.vercel.app/mcp` | `POST`, `GET`, `DELETE` | Discovery **FREE**; paid `tools/call` via **x402** | Stateless MCP Streamable HTTP endpoint |
| `https://merchant-scam-guard-mcp.vercel.app/llms.txt` | `GET` | **FREE** | Dynamic agent discovery document synchronized with live tool pricing |
| `https://merchant-scam-guard-mcp.vercel.app/.well-known/mcp.json` | `GET` | **FREE** | Machine-readable MCP server card manifest |
| `https://merchant-scam-guard-mcp.vercel.app/health` | `GET` | **FREE** | Liveness check |

---

## Free MCP Discovery Primitives ($0.00)

Agents can inspect all capabilities, pricing, and schemas without paying:

- **Protocol methods:** `initialize`, `ping`, `tools/list`
- **Resources (`resources/list`, `resources/read`):**
  - `guard://pricing`
  - `guard://risk-rubric`
  - `guard://schema/verdict`
  - `guard://llms.txt`
- **Prompts (`prompts/list`, `prompts/get`):**
  - `pre_purchase_safety_check`
  - `checkout_redirect_audit`
  - `refund_policy_due_diligence`

---

## Paid MCP Tools (x402 USDC on Base)

| Tool | Price (USDC on Base) | Description |
| :--- | :--- | :--- |
| `verify_merchant_trust` | **$0.01** | Parallel live checks across RDAP, TLS certificate inspection, `crt.sh`, URLhaus (`abuse.ch`), Cloudflare Radar, and refund policy probe. Returns a `0–100` risk score and `ALLOW` / `CAUTION` / `BLOCK` verdict. |
| `inspect_checkout_url` | **$0.005** | SSRF-hardened redirect chain tracer (up to 5 hops), cross-domain hijacking detection, IDN/punycode spoofing check, raw card form detection, payment processor fingerprinting, live TLS, and URLhaus lookup. |
| `extract_refund_policy_summary` | **$0.005** | Discovers, sanitizes (prompt-injection isolated), and extracts structured refund/return policy terms and scam template red flags. |

---

## License

**All Rights Reserved.** See [LICENSE](./LICENSE). This repository contains public documentation and registry manifests for the hosted remote MCP service only.
