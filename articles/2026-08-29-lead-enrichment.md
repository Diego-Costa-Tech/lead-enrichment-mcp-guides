# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your development environment. By integrating a dedicated B2B lead enrichment MCP server, you enable Cursor and VS Code Copilot to perform real-time company profile lookups and technographic scouting using standardized, type-safe Model Context Protocol tools.

## Core Features of the Enrichment MCP
This server acts as a bridge between high-reasoning LLMs and deep-web corporate data silos. It implements a strictly typed interface to ensure that agents do not hallucinate company attributes or contact details.

*   **Deep Firmographics:** Access real-time data including employee counts, revenue brackets, industry classifications, and headquarters locations.
*   **Technographic Intelligence:** Identify a lead's current tech stack—from CRM usage (Salesforce, HubSpot) to cloud infrastructure (AWS, GCP) and frontend frameworks.
*   **Active Intent Signals:** Retrieve signals based on recent funding rounds, hiring trends, and news events to prioritize high-value outreach.
*   **Zod-Enforced Parameters:** Every tool in the MCP server uses strict Zod schema annotations, forcing the LLM to provide valid domain formats and preventing the parameter hallucinations common in standard REST tool-calling.

## Configure Your IDE (Cursor / VS Code / Claude Desktop)
To give your AI coding assistant or sales agent access to live data, add the following configuration to your `project.json` or global MCP settings:

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Real-Time JSON-RPC Response Example
When you ask an agent like Cursor to "Analyze the tech stack of stripe.com," the MCP server returns a structured JSON-RPC payload. This clean data structure allows the LLM to reason accurately without parsing messy HTML.

```json
{
  "tool_use": "enrich_lead",
  "result": {
    "companyName": "Stripe, Inc.",
    "industry": "Fintech / Payments",
    "technographics": ["React", "Ruby on Rails", "AWS", "Salesforce"],
    "intentSignals": {
      "hiring": "High",
      "recentFunding": "Series I",
      "growthScore": 0.94
    },
    "confidenceScore": 0.98,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing for AI Agents
Traditional data providers demand massive upfront contracts, but the B2B Lead Enrichment MCP API is built for the agentic era. It utilizes a **Risk-Free Metered Billing** structure specifically designed for autonomous SDR swarms. You are only billed for successful enrichments where the **Confidence Score > 0.6**. If the server returns a low-quality match or fails to find the record, the query cost is exactly $0. This allows developers to build high-volume lookup scripts and agentic loops without the risk of burning through budgets on "hallucinated" or missing data.

## Get Your Free Enrichment API Key
Ready to upgrade your AI agents with live B2B intelligence? Visit the documentation to grab your API key and start enriching leads with a single JSON-RPC call.

[Get Started at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)