# How to Give Cursor and Claude Desktop Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and real-time intent data without custom middleware is by deploying an MCP-native B2B lead enrichment server directly into your development environment. By leveraging the Model Context Protocol (MCP), developers can now inject high-fidelity company profiles and intent signals directly into Claude Desktop or Cursor, effectively turning an AI agent into an autonomous prospect research engine.

## Core Features
The B2B lead enrichment MCP server provides specialized tools that allow models to query deep data layers, including:
*   **Firmographics:** Real-time company sizing, HQ location, and executive leadership data.
*   **Technographics:** Detailed tech stack insights and software utilization patterns.
*   **Intent Signals:** Proprietary intent markers derived from web activity and market research.
*   **Hallucination Prevention:** All tool parameters utilize strict **Zod annotations** and schema validation, ensuring the LLM passes required inputs in the exact format required by the upstream provider.

## Configuring Your Environment
To integrate this directly into your local AI workspace, add the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings. The server natively supports the JSON-RPC protocol over standard I/O.

```json
{
  "mcpServers": {
    "lead-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/lead-enrichment-mcp"],
      "env": {
        "LEAD_ENRICHMENT_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## Example Tool Response Payload
When the LLM triggers the `enrich_lead` tool, it receives a highly structured, machine-readable JSON-RPC response. This ensures your agent agents operate on verified data rather than model training weights:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Snowflake"],
    "intentSignals": ["hiring_spike", "recent_funding_round"],
    "confidenceScore": 0.92,
    "lastUpdated": "2023-10-27T10:00:00Z"
  },
  "id": 1
}
```

## Risk-Free Metered Billing
We prioritize developer ROI by implementing a **Confidence-Based Billing model**. You are only charged for successful enrichments where the `confidenceScore` exceeds 0.6. Any data return that falls below the quality threshold or results in a failure to locate the entity is billed at $0. This ensures your autonomous SDR swarms remain cost-effective while scaling prospecting operations.

## Get Started with MCP Lead Enrichment
Ready to turn your AI agents into top-tier prospectors? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and start utilizing our production-ready MCP server on the free tier today.