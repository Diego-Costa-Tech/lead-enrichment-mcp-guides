# Building Cost-Effective Autonomous SDR Swarms with Metered B2B Lead Enrichment MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your agentic workflow. This architecture allows autonomous SDR swarms to perform real-time lead qualification and enrichment using the Model Context Protocol, ensuring that every outreach attempt is backed by verified company profiles and technographic data.

## Core Features
The B2B Lead Enrichment MCP API provides a robust set of tools designed for high-autonomy agentic workflows. By leveraging the **Model Context Protocol (MCP)**, this server exposes deep data layers that allow agents to understand the "who, what, and why" of a prospect instantly.

*   **Deep Firmographics:** Access real-time data on company size, revenue brackets, industry classification, and headquarters location.
*   **Technographic Intelligence:** Identify the prospect's tech stack, including CRM usage, cloud providers, and marketing automation tools.
*   **Dynamic Intent Signals:** Fetch recent growth indicators and hiring trends to trigger timely outreach.
*   **Hallucination Prevention:** All tool parameters use strict **Zod schema annotations**. This forces the LLM to adhere to valid JSON-RPC structures, eliminating the "parameter hallucination" common in loose API integrations.

## Implementation: Claude Desktop & Cursor Configuration
To give your local AI agent (like Claude Desktop or Cursor) the ability to research companies, add the following configuration to your `claude_desktop_config.json` or your MCP settings file:

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
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Enrichment Response Example
When an agent calls the `enrich_lead` tool, the MCP server returns a structured JSON-RPC response. This data is injected directly into the LLM's context window, allowing it to reason about the lead with high precision.

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": {
      "domain": "stripe.com"
    }
  },
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Stripe",
          "industry": "Fintech / Payments",
          "headcount": "7,000+",
          "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
          "intentSignals": ["Expansion into EU markets", "High hiring volume in Engineering"],
          "confidenceScore": 0.98,
          "is_qualified": true
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing for SDR Swarms
Scaling an autonomous SDR swarm can be expensive if you pay for every API call, regardless of data quality. This MCP server solves the cost bottleneck through **Risk-Free Metered Billing**. 

Your account is only debited when the engine provides high-utility data. Specifically, you are billed only for successful enrichments that return a **Confidence Score > 0.6**. If the data is unavailable, the confidence score is low, or the query fails, the cost is exactly **$0**. This allows developers to build aggressive "loop-and-search" agents that can scan thousands of domains without the risk of massive bills for "no-match" results.

## Get Your Free API Key Today
Ready to upgrade your AI sales agents with real-time B2B intelligence? You can start building immediately with our free tier.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and connect your MCP-compatible LLM in seconds.**