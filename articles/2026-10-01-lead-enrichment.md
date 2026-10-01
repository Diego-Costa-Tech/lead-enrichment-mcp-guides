# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to real-time B2B firmographics and intent data without custom middleware is by deploying an MCP-native B2B lead enrichment MCP server directly into your IDE. By leveraging the Model Context Protocol, developers can now ground their autonomous sales agents in live company profiles, technographics, and intent signals, effectively eliminating the data lag associated with static training sets.

## Core Features and Technical Integrity
This MCP server exposes a standardized interface for agents to query **firmographic data**, **technographic stacks**, and **real-time intent signals**. To solve the common issue of LLM parameter hallucinations, the API utilizes **strict Zod-schema annotations** for all tool arguments. This ensures that when the LLM triggers an enrichment call, the input parameters are validated against strict data types before the request ever hits the network.

- **Firmographic Data:** Access HQ location, revenue bands, and employee counts.
- **Technographic Insights:** Identify specific SaaS tools and infrastructure used by target accounts.
- **Intent Signals:** Filter by high-probability buying signals based on real-time web activity.
- **Hallucination Prevention:** Enforced Zod schemas ensure zero-shot reliability in complex agentic workflows.

## Configuration for Cursor and VS Code
To integrate the B2B Lead Enrichment MCP API, add the following configuration to your `mcp.json` settings file (or your IDE's MCP configuration panel):

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/lead-enrichment-mcp"
      ],
      "env": {
        "API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## Standardized JSON-RPC Enrichment Response
The tool returns a clean, structured JSON-RPC object, making it trivial for agents to parse data into CRM objects or outreach drafts:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Datadog"],
    "intentSignals": ["high", "Q3-buying-intent"],
    "confidenceScore": 0.92,
    "revenueRange": "$50M-$100M"
  },
  "id": 1
}
```

## Risk-Free Metered Billing
Efficiency in agentic workflows requires cost-effective operations. Our pricing model is designed for high-scale SDR swarms: you are only billed for successful enrichments where the **Confidence Score > 0.6**. Queries that fail to meet this threshold or return low-quality matches cost you exactly $0. This ensures your budget is only consumed by high-intent, actionable intelligence.

## Get Started Today
Stop wasting time on stale contact data and manual lookups. Integrate professional-grade B2B intelligence into your AI agent environment today. Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly.