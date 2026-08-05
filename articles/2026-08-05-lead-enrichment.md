# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give AI IDEs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your development environment. This integration allows Cursor and VS Code Copilot to utilize the Model Context Protocol (MCP) to fetch real-time company profiles, technographic stacks, and growth signals during the coding or research process.

## Core Features
The B2B Lead Enrichment MCP API provides a structured interface for LLMs to interact with complex organizational data. By leveraging **Zod-annotated schemas**, the server enforces strict parameter validation, which effectively eliminates the common "hallucination" problem where AI agents invent company metadata.

*   **Firmographic Intelligence:** Deep-tier data including revenue brackets, headcount growth, and HQ geolocation.
*   **Technographic Stack Detection:** Identify the specific SaaS tools, cloud providers, and development frameworks used by a target organization.
*   **Real-time Intent Signals:** Access live data points such as active job listings, recent funding rounds, and product launches.
*   **Native Tool Integration:** Built specifically for the Model Context Protocol, ensuring compatibility with Claude Desktop, Cursor, and any MCP-enabled agent.

## Configuration for Cursor and Claude Desktop
To enable these capabilities, add the following configuration to your `cursor.json` or Claude Desktop configuration file. This connects your environment to the production-ready MCP endpoint.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Example
When the LLM invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This data is injected directly into the conversation context, allowing the agent to reason about the company with high precision.

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
    "companyName": "Stripe, Inc.",
    "industry": "Fintech / Payments",
    "technographics": ["AWS", "React", "Ruby on Rails", "Kubernetes"],
    "intentSignals": {
      "hiringTrend": "Aggressive",
      "recentNews": "Expanding global tax automation suite"
    },
    "confidenceScore": 0.98,
    "metadata": {
      "lastUpdated": "2023-10-27T14:30:00Z"
    }
  }
}
```

## Risk-Free Metered Billing
Most data APIs charge for every request, regardless of data quality. This MCP server utilizes a **Risk-Free Metered Billing** structure specifically designed for autonomous AI workflows. Your account is only billed for successful enrichments that return a `confidenceScore` greater than 0.6. If the data is low-quality, the result is unavailable, or the confidence is too low for reliable AI decision-making, the query cost is $0.

## Get Your Free API Key Today
Ready to empower your AI agents with real-world B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start building with the free tier today.