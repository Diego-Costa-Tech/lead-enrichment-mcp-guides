# Eliminating LLM Parameter Hallucinations in B2B Sales Agents with Native MCP Tools

To eliminate parameter hallucinations and data leakage in automated sales workflows, developers are adopting the Model Context Protocol (MCP) to provide LLMs with strict, schema-validated access to live B2B firmographics and intent data. By implementing a native B2B lead enrichment MCP server, agents can query real-time company profiles using Zod-backed schemas that ensure valid inputs and high-fidelity JSON-RPC outputs.

## Core Features

Standardizing data retrieval through the Model Context Protocol allows for a deterministic interaction between the LLM and external data sources. This specific MCP implementation provides several key data layers:

*   **Strict Zod Schema Enforcement:** Every tool input, such as `domain` or `company_name`, is validated against strict TypeScript/Zod schemas before the API call is executed, preventing the LLM from passing "invented" parameters or malformed strings.
*   **Deep Firmographic Mapping:** Retrieve verified headcount, revenue ranges, industry NAICS codes, and headquarters geolocation.
*   **Technographic Stack Detection:** Identify a company’s current software stack (e.g., Salesforce, AWS, Marketo) to trigger relevant sales playbooks.
*   **Intent Signal Processing:** Access real-time signals indicating a company’s propensity to buy, filtered through a proprietary confidence algorithm.
*   **Native Tool Integration:** Directly compatible with Claude Desktop, Cursor, and VS Code Copilot without requiring custom proxy middleware or brittle "function calling" glue code.

## MCP Configuration for Claude Desktop & Cursor

To integrate these tools into your development environment or sales agent, add the following configuration to your `claude_desktop_config.json` or your specific MCP settings file:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-b2b-enrichment"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## Validated JSON-RPC Response Example

When your agent invokes the `enrich_lead` tool, the MCP server returns a structured JSON-RPC payload. This structure ensures the LLM receives the data in a format it can parse with 100% accuracy, significantly reducing "hallucinated" company details.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Example Tech Corp",
    "industry": "Enterprise Software",
    "technographics": ["Kubernetes", "Snowflake", "Okta"],
    "intentSignals": [
      { "type": "funding_round", "score": 0.92, "date": "2023-10-15" },
      { "type": "hiring_surge", "score": 0.85, "date": "2023-11-01" }
    ],
    "confidenceScore": 0.98,
    "source": "verified_registry"
  },
  "id": 1
}
```

## Risk-Free Metered Billing

This MCP server utilizes a developer-first, risk-free metered billing structure designed for autonomous agent swarms. Unlike traditional APIs that charge for every request regardless of quality, this server only bills for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the record is not found, or the confidence is too low to be actionable, the query cost is $0. This allows for high-volume scanning and lead qualification without the risk of burning through budgets on empty results.

## Get Started with Free B2B Lead Enrichment

Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start grounding your sales agents in real-time, verified firmographic data today.