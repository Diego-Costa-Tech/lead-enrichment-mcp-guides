# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

To eliminate data staleness and manual research in AI-driven development or sales-ops workflows, you can connect Cursor or VS Code to a live B2B lead enrichment MCP server using the Model Context Protocol. This integration allows your AI agent to fetch real-time company profiles, technographics, and intent signals directly within your IDE or agentic framework using a single, schema-validated tool call.

## Core Features

The B2B Lead Enrichment MCP API provides a robust bridge between LLM interfaces and live market intelligence. Unlike static databases that often lead to parameter hallucinations, this server utilizes strict **Zod-validated schemas** to ensure that agents like Claude or Cursor receive structured, typed data every time.

*   **Real-Time Firmographics:** Access up-to-the-minute data on company size, revenue brackets, industry classification, and headquarters location.
*   **Deep Technographics:** Identify the software stack of a target lead, including CRM usage, cloud providers, and marketing automation tools.
*   **Intent Signals & Market Context:** Retrieve hiring trends and recent funding news to empower your AI agent to write hyper-personalized outreach or perform competitive analysis.
*   **Hallucination Prevention:** By defining tools with explicit JSON-RPC parameters, the LLM is constrained to valid query formats, significantly reducing the frequency of incorrect or "guessed" company data.

## Configuration for Cursor or Claude Desktop

To give your AI agent access to these tools, add the following configuration to your `project.json` or your global MCP settings file (e.g., `claude_desktop_config.json`):

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

When your agent calls the `enrich_lead` tool, it receives a clean, machine-readable payload. This structure allows the LLM to parse specific data points without getting lost in unstructured text:

```json
{
  "tool_name": "enrich_lead",
  "response": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "headcount": "500-1000",
    "technographics": ["Salesforce", "AWS", "Segment", "React"],
    "intentSignals": {
      "hiringTrend": "Increasing",
      "recentNews": "Series C funding closed"
    },
    "confidenceScore": 0.94,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing

This MCP server is built for cost-effective AI operations. We implement a **Risk-Free Metered Billing** structure where you are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server cannot find high-quality data or the query fails to meet the quality threshold, the cost is exactly $0. This ensures that autonomous SDR swarms and data pipelines remain ROI-positive even when processing large, messy datasets.

## Get Your Free MCP API Key Now

Ready to supercharge your AI agents with real-time B2B data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on our free tier and start enriching leads directly within Cursor, VS Code, or Claude Desktop.