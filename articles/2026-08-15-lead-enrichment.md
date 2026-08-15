# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Integrating real-time B2B data directly into your IDE's AI agents is now possible by deploying a Model Context Protocol (MCP) server that provides native access to firmographic and intent data. By connecting an MCP-native B2B lead enrichment API server to your LLM configuration, you eliminate the need for brittle middleware while ensuring your coding assistants have immediate context on company profiles, technographics, and buying intent signals.

## Core Features and Data Integrity
Our MCP server bridges the gap between static LLM knowledge and live market data. By utilizing **strict Zod schema annotations** for every tool definition, we effectively force LLMs to adhere to required parameter structures, which virtually eliminates common parameter hallucinations that plague traditional API integrations.

The server provides granular access to:
*   **Firmographics:** Real-time headcount, revenue, and location data.
*   **Technographics:** Current software stack and infrastructure insights.
*   **Intent Signals:** Current market activity and lead priority scores.

## Configuration for Cursor or Claude Desktop
To integrate the B2B lead enrichment tool, add the following entry to your `claude_desktop_config.json` or your Cursor MCP settings. This configuration mounts the API server directly into the agent's tool-use environment.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-lead-enrichment",
        "--api-key",
        "YOUR_API_KEY_HERE"
      ],
      "env": {
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Payload
When an LLM invokes the `enrich_lead` tool, the server returns a strongly-typed JSON-RPC response designed for high-context ingestion.

```json
{
  "jsonrpc": "2.0",
  "id": "req-12345",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": {
      "score": 88,
      "category": "High Intent - Pricing Page Visit"
    },
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing
Efficiency in agentic workflows is paramount. Our service features a unique risk-free metered billing structure: you are only billed for successful enrichments where the **Confidence Score exceeds 0.6**. If our models return a low-confidence or failed result, that query costs $0, allowing you to scale your autonomous SDR swarms without worrying about wasted token or API spend on junk data.

## Get Your API Key
Ready to equip your development environment with production-grade B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start building on our free tier immediately.