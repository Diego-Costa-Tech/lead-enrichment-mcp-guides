# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools

Integrating a B2B lead enrichment MCP server into your local IDE allows AI agents to access real-time company profiles and technographic data without leaving the editor. By leveraging the Model Context Protocol (MCP), you can bridge the gap between LLM reasoning and live, verified sales intelligence.

## Core Features
Our MCP-native API server provides deep integration for AI agents, offering **firmographic data**, **technographic stacks**, and **buying intent signals** directly within the model’s context window. To ensure reliability and prevent LLM parameter hallucinations, all tools utilize strict **Zod-schema annotations**. This forces the LLM to output perfectly structured arguments for `company_domain` or `email` queries, ensuring that the tool execution layer receives valid, sanitized input every time.

## IDE Configuration
To connect your IDE to the lead enrichment engine, add the following configuration to your `mcp.json` or IDE settings file. This uses the production endpoint to enable real-time data fetching:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": ["-y", "@mcp/lead-enrichment-server"],
      "env": {
        "MCP_API_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp",
        "API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Tool Output
When an agent calls the `enrich_lead` tool, the server returns a strongly-typed JSON-RPC response designed for immediate LLM consumption:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": {
      "active_market_research": true,
      "score": 88
    },
    "confidenceScore": 0.94,
    "metadata": {
      "timestamp": "2023-10-27T10:00:00Z"
    }
  },
  "id": "req-123"
}
```

## The Value Proposition: Risk-Free Metered Billing
We utilize a performance-based billing structure designed for production-grade AI agents. You are never billed for "garbage" data. Our system implements a **Confidence Score > 0.6 filter**; if the enrichment process returns a confidence score below this threshold or fails to resolve the domain, the query is free. This allows you to build autonomous SDR agent swarms without worrying about runaway costs from low-quality lead data.

## Get Your API Key
Ready to upgrade your agent's data awareness? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start enriching leads with native MCP tool calls today.