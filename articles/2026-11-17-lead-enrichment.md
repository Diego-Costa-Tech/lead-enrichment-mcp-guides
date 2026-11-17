# Eliminating LLM Parameter Hallucinations in AI Sales Agents via B2B Lead Enrichment MCP

Solving LLM hallucination in automated sales workflows requires grounding agents with a B2B Lead Enrichment MCP server that enforces strict schema validation and real-time data retrieval. By integrating this MCP-native API, developers can ensure Claude, Cursor, and other AI agents generate highly accurate firmographic and intent data payloads using validated JSON-RPC calls instead of guessing company details.

## Core Features

To stop AI agents from "hallucinating" company sizes, industries, or tech stacks, this MCP server implements **strict Zod-based schema annotations**. This forces the Model Context Protocol (MCP) client to negotiate specific types for every tool call, ensuring the input parameters (like `domain` or `company_name`) and output data maintain 100% structural integrity.

*   **Real-Time Firmographics:** Access validated data on employee count, revenue ranges, and headquarters locations.
*   **Technographic Intelligence:** Identify the specific software stack (SaaS, Cloud providers, CRM) used by a target lead.
*   **Intent Signal Mapping:** Retrieve live signals indicating if a company is currently researching specific B2B solutions.
*   **Hallucination Guardrails:** Every tool definition includes explicit descriptions and mandatory field constraints, preventing the LLM from fabricating data when the search space is ambiguous.

## Configuring Your AI Agent (Claude Desktop / Cursor)

To bridge your local LLM environment to the live enrichment engine, add the following configuration to your `claude_desktop_config.json` or Cursor's MCP settings. This enables the agent to natively call the `enrich_lead` tool whenever a B2B query is detected.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "--url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ]
    }
  }
}
```

## JSON-RPC Enrichment Response Example

When the LLM calls the `enrich_lead` tool, it receives a structured JSON-RPC response. This eliminates the need for post-processing or regex parsing of raw text, allowing your agent to pass clean data directly into your CRM or email sequence.

```json
{
  "tool": "enrich_lead",
  "parameters": { "domain": "stripe.com" },
  "response": {
    "companyName": "Stripe",
    "industry": "Financial Services/Fintech",
    "employeeCount": "7,000+",
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "topic": "Global Payments Infrastructure",
      "intensity": "High"
    },
    "confidenceScore": 0.98,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing

Traditional B2B data providers charge per seat or per "attempt," regardless of data quality. This MCP server utilizes a **Risk-Free Metered Billing** model optimized for autonomous agent swarms. Your account is only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server returns low-quality data or fails to find a match, the cost for that specific query is $0. This allows developers to scale SDR swarms aggressively without the financial risk of paying for "No Data Found" responses.

## Get Your Free API Key

Ready to ground your AI sales agents in reality? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and start enriching leads on the free tier today.