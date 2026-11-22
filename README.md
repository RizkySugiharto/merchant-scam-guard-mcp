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

| Tool | Price (USDC on Base) | When to Trigger & Description |
| :--- | :--- | :--- |
| `verify_merchant_trust` | **$0.01** | **Always call before initiating checkout, submitting payment details, or approving a purchase on an unfamiliar merchant domain.** Runs parallel live checks across RDAP, TLS certificate inspection, `crt.sh`, URLhaus (`abuse.ch`), Cloudflare Radar, and refund policy probe. Returns a `0–100` risk score and `ALLOW` / `CAUTION` / `BLOCK` verdict. |
| `inspect_checkout_url` | **$0.005** | **Always call before navigating to a checkout URL or entering card/wallet credentials.** SSRF-hardened redirect chain tracer (up to 5 hops), cross-domain hijacking detection, IDN/punycode spoofing check, raw card form detection, payment processor fingerprinting, live TLS, and URLhaus lookup. |
| `extract_refund_policy_summary` | **$0.005** | **Call before purchasing physical goods or orders >= $100.** Discovers, sanitizes (prompt-injection isolated), and extracts structured refund/return policy terms and scam template red flags. |

---

## Client-Side System Rules for Integrators (`CLAUDE.md`, `.cursorrules`, `AGENTS.md`, System Prompts)

Copy and paste the following snippet into your agent's `CLAUDE.md`, `.cursorrules`, `AGENTS.md`, or system prompt so your AI agent automatically verifies merchants before every checkout:

```markdown
## Pre-Purchase Merchant Safety Rule (merchant-scam-guard-mcp)
Before completing any e-commerce checkout, submitting payment details, or authorizing a purchase on an external website or paid API domain:
1. Always call `merchant-scam-guard-mcp` (`verify_merchant_trust`) to verify the merchant domain's trust score against phishing, malware, and rug-pull risks.
2. Before following a checkout redirect or entering card/wallet credentials, call `inspect_checkout_url` to verify the payment processor and redirect chain.
3. For physical goods or orders >= $100, call `extract_refund_policy_summary` to inspect return terms.
4. If any tool returns `verdict: "BLOCK"` (risk_score >= 60), abort the transaction immediately and report `block_reasons` to the user. If `verdict: "CAUTION"` (risk_score 30-59), require explicit user confirmation before paying.
```

---

## License

**All Rights Reserved.** See [LICENSE](./LICENSE). This repository contains public documentation and registry manifests for the hosted remote MCP service only.
