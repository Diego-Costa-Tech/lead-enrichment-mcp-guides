# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to inject real-time B2B firmographics into your local AI development environment is by deploying a B2B lead enrichment MCP server directly into your IDE’s context providers. By leveraging the Model Context Protocol, developers can grant Cursor or VS Code native access to live company profiles and intent signals, effectively eliminating manual research workflows and data entry friction.

## Core Features and Data Integrity
Our MCP-native API server bridges the gap between raw web-scale data and LLM reasoning engines. It delivers structured **firmographic data** (revenue, headcount, location), **technographic insights** (SaaS stack, infrastructure providers), and **real-time intent signals** (hiring trends, product launches). 

To solve the perennial issue of LLM parameter hallucinations, we utilize strict **Zod-based schema annotations** in our tool definitions. This ensures that the model provides correctly formatted domains and company names, as the server-side validator rejects malformed inputs before the enrichment query ever reaches the data provider.

## Connecting Cursor to the MCP API
To enable the tool, add the following configuration to your `mcp.json` file. This allows Cursor to execute `enrich_lead` queries directly from the chat interface.

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
        "LEAD_ENRICHMENT_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## Expected JSON-RPC Tool Output
When the LLM triggers the `enrich_lead` tool, it receives a clean, deterministic JSON response, enabling high-precision reasoning in your autonomous SDR agents:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Datadog"],
    "intentSignals": {
      "hiringTrend": "aggressive",
      "recentFunding": "Series C"
    },
    "confidenceScore": 0.94
  },
  "id": "req-123"
}
```

## Risk-Free Metered Billing
We prioritize developer ROI by implementing a **Confidence-Based Billing model**. Our infrastructure tracks the `confidenceScore` of every lookup; if the data provider returns a result with a confidence score of 0.6 or lower, or if the query fails to return actionable firmographics, you are not charged. You only pay for high-quality, actionable B2B intelligence, making this the most cost-effective way to scale autonomous sales swarms.

## Start Building Today
Ready to integrate production-grade B2B data into your AI agents? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching your leads in seconds.