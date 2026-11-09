# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server. By connecting Claude Desktop directly to the B2B Lead Enrichment MCP API, developers can transform a static chat interface into a powerful research agent capable of fetching real-time company profiles and technographic data using the Model Context Protocol.

## Core Features

This MCP server provides a standardized interface for LLMs to query deep organizational data points. Unlike traditional REST API integrations that require manual glue code, this server uses **Zod-annotated schemas** to define its toolset, allowing Claude or Cursor to understand exactly which parameters are required for a successful query.

*   **Real-time Firmographics:** Access dynamic data including employee counts, revenue brackets, and industry classifications.
*   **Technographic Stack Mapping:** Identify the underlying technologies (SaaS, Cloud providers, CRM systems) used by a target organization.
*   **Intent & Market Signals:** Retrieve high-signal data points regarding company growth and hiring trends.
*   **Hallucination Prevention:** The server uses strict JSON-RPC communication and schema validation to ensure the LLM only passes valid, verified domains and identifiers.

## Quickstart: Claude Desktop Configuration

To enable these tools in Claude Desktop, add the following configuration to your `claude_desktop_config.json` file. This tells Claude how to connect to the remote MCP endpoint via a standard SSE (Server-Sent Events) transport layer.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_ACTUAL_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Tool Response Example

When the LLM invokes the `enrich_lead` tool, the MCP server returns a structured payload. This clean data structure allows the model to summarize insights or generate outreach copy without parsing messy HTML or unstructured text.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "ExampleCorp",
    "industry": "Enterprise Software",
    "technographics": ["AWS", "Salesforce", "Kubernetes", "React"],
    "intentSignals": {
      "hiringTrend": "Aggressive",
      "newMarketEntry": "EMEA"
    },
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Performance-Driven Metered Billing

Unlike traditional B2B data providers that charge for every API call regardless of quality, this MCP server utilizes a **Risk-Free Metered Billing** model. The system calculates a `confidenceScore` for every enrichment. You are only billed for successful data retrievals where the Confidence Score exceeds 0.6. Any query that results in low-confidence data or a "not found" status is processed at $0 cost, making it the most cost-effective solution for building autonomous SDR swarms and high-volume AI research agents.

## Get Your Free API Key Instantly

Ready to empower your LLM with real-time B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start using the B2B Lead Enrichment MCP API on our free tier today.