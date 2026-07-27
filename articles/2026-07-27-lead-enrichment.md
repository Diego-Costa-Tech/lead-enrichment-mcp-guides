# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

To eliminate manual data lookups during sales-tech development, you can now equip Cursor and VS Code with a native B2B lead enrichment MCP server for real-time company profiles and intent data. This implementation uses the Model Context Protocol to bridge the gap between your LLM-based IDE and live firmographic APIs, ensuring your AI agents have ground-truth data for every domain they encounter.

## Core Features
The B2B Lead Enrichment MCP API provides a robust data layer directly to your LLM’s context window, featuring:
- **Comprehensive Firmographics:** Access deep metadata including headcount ranges, revenue estimates, and global headquarters locations.
- **Technographic Intelligence:** Identify the exact software stack (e.g., CRM, Cloud Provider, Analytics) a target company currently utilizes.
- **Real-Time Intent Signals:** Retrieve high-intent data points that indicate when a company is actively searching for specific solutions.
- **Strict Zod Schema Enforcement:** All tool parameters are strictly typed using Zod annotations, which forces the LLM to follow precise JSON structures and effectively eliminates parameter hallucinations during tool calling.

## Configuration for Claude Desktop and Cursor
To connect your environment to the production MCP server, add the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-lead-enrichment"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Example
When your AI agent invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This ensures the LLM can parse the data without guessing:

```json
{
  "tool": "enrich_lead",
  "content": [
    {
      "type": "text",
      "text": {
        "companyName": "ExampleCorp",
        "industry": "Enterprise Software",
        "technographics": ["Salesforce", "AWS", "Segment"],
        "intentSignals": ["High research activity in 'Cloud Security'"],
        "confidenceScore": 0.94,
        "employeeCount": 500,
        "isVerified": true
      }
    }
  ]
}
```

## Risk-Free Metered Billing
Most B2B data providers charge for every API call, regardless of data quality. This MCP server utilizes a **Confidence-First Billing** model. Your account is only debited for successful enrichments where the **Confidence Score is > 0.6**. If the server returns low-confidence data, a "not found" status, or a failed query, the cost is exactly $0. This allows developers to build high-volume SDR swarms and autonomous agents without the risk of burning through budgets on hallucinations or stale data.

## Get Started with the B2B Lead Enrichment MCP
Ready to give your AI agents native access to the global business graph? Visit our portal to grab your free API key and view the full documentation.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to get your API key today.**