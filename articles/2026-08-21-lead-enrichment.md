# How to Give Cursor and VS Code Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your IDE's context. By leveraging a B2B lead enrichment MCP server, developers can transform Cursor or VS Code into powerful sales engineering assistants that query real-time company profiles using standardized JSON-RPC protocols.

## Core Features
This MCP implementation provides a deep-data layer for AI agents, ensuring that every query is backed by verifiable business intelligence. Unlike generic search tools, this server uses **Strict Zod Schema validation** to enforce parameter types, which effectively eliminates LLM parameter hallucinations during tool calling.

*   **Real-time Firmographics:** Instant access to **employee counts, revenue brackets, and industry classifications**.
*   **Deep Technographics:** Identify the prospect's tech stack, including their **CRM, cloud infrastructure, and marketing automation tools**.
*   **Actionable Intent Signals:** Track **funding rounds, recent leadership changes, and hiring trends** to identify high-propensity targets.
*   **Agent-Optimized Responses:** Clean, token-efficient JSON payloads designed for high-context LLM reasoning.

## IDE Configuration
To enable these tools in **Cursor** or **Claude Desktop**, add the following configuration to your settings. This connects your environment to the production MCP endpoint, allowing the LLM to call the `enrich_lead` tool whenever you mention a company or domain.

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
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Example
When the LLM invokes the `enrich_lead` tool, it receives a structured payload. This allows the model to synthesize high-quality outreach or technical discovery documents based on factual data rather than "guessing" company details.

```json
{
  "tool": "enrich_lead",
  "result": {
    "companyName": "ExampleCorp",
    "industry": "Enterprise SaaS",
    "technographics": ["Salesforce", "AWS", "Segment"],
    "intentSignals": [
      {"type": "Funding", "value": "Series C", "date": "2023-11-15"}
    ],
    "confidenceScore": 0.98,
    "source": "verified_aggregator"
  }
}
```

## Risk-Free Metered Billing
Traditional data APIs charge for every request, regardless of whether they find a match. This B2B Lead Enrichment MCP API utilizes a developer-friendly **Risk-Free Metered Billing** model. You are only billed for successful enrichments that return a **Confidence Score greater than 0.6**. If the server returns "No Data Found" or a low-confidence match, the request cost is exactly $0, making it the most cost-effective solution for building autonomous SDR swarms and high-volume sales agents.

## Get Your Free API Key
Ready to upgrade your AI agent's business intelligence? Visit the link below to generate your API key and start querying live firmographic data in minutes.

[Get Started at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)