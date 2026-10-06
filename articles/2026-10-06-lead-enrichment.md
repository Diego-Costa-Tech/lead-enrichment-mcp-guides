# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server. By integrating our B2B lead enrichment MCP server directly into your Claude Desktop or Cursor environment, you enable real-time company profiles and decision-maker contact intelligence via standardized JSON-RPC protocols.

## Core Features
Our MCP server bridges the gap between LLM reasoning and structured B2B datasets. It provides deep access to:
*   **Firmographic Data:** Headcount, annual revenue, and HQ location.
*   **Technographic Layers:** Existing software stack, CMS, and CRM integrations.
*   **Intent Signals:** Real-time buying intent and trending topics for specific domains.
*   **LLM Safety:** All tool parameters are defined using **strict Zod schemas**, which forces the LLM to adhere to correct input formats, drastically reducing parameter hallucinations and API request errors.

## MCP Client Configuration
To connect this to Claude Desktop, add the following to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "lead-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/lead-enrichment-mcp"],
      "env": {
        "API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Example
When the LLM invokes the `enrich_lead` tool, it receives a normalized, high-fidelity JSON-RPC response structured for immediate agent processing:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": ["high_intent_cloud_migration", "q3_budget_allocation"],
    "confidenceScore": 0.92,
    "employeeCount": "500-1000"
  }
}
```

## The Value Proposition: Risk-Free Metered Billing
Most B2B data providers charge per request regardless of the data quality. Our API implements a "Pay-for-Performance" model: you are only billed for successful enrichments where the **Confidence Score exceeds 0.6**. If our system returns low-quality data or fails to identify the entity, the request cost is $0. This ensures that your autonomous SDR swarms remain cost-effective while maximizing the precision of your lead generation pipeline.

## Get Your API Key
Ready to upgrade your AI agent's firmographic intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start integrating the B2B Lead Enrichment MCP API into your development workflow for free today.