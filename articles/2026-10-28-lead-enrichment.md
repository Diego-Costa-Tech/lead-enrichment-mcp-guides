# How to Equip Cursor and VS Code with Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your IDE. By connecting Cursor or VS Code to a B2B lead enrichment MCP server, developers enable AI agents to fetch real-time company profiles, technographic stacks, and buying signals using standardized Model Context Protocol tools.

## Core Features

The B2B Lead Enrichment MCP API provides a structured interface for AI agents to query high-fidelity business data. By leveraging the Model Context Protocol, the server exposes tools that integrate directly into the LLM's reasoning loop:

*   **Deep Firmographic Data**: Instantly retrieve **companyName**, **industry**, **employeeCount**, and **headquartersLocation**.
*   **Technographic Intelligence**: Identify the software and infrastructure used by a target company to tailor technical outreach or product integration scripts.
*   **Real-Time Intent Signals**: Access signals that indicate a company’s current growth stage or technology shifts.
*   **Strict Schema Validation**: Every tool, such as `enrich_lead`, utilizes **Zod-annotated parameters** (e.g., requiring a valid `domain` or `email`). This ensures the LLM provides valid inputs and virtually eliminates parameter hallucinations common in standard REST API calls.

## IDE Configuration

To enable these tools in your AI-powered IDE, add the following configuration to your `project.json` (for Cursor) or your MCP settings file:

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
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Tool Response Example

When your agent invokes the `enrich_lead` tool, it receives a structured JSON-RPC response. This clean data allows the LLM to synthesize outreach or perform competitive analysis with high accuracy:

```json
{
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["Kubernetes", "AWS", "Terraform", "PostgreSQL"],
    "intentSignals": [
      { "type": "Hiring", "strength": 0.8, "department": "DevOps" }
    ],
    "firmographics": {
      "employeeCount": 500,
      "location": "San Francisco, CA"
    },
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing

This MCP server is designed for production-grade SDR swarms and developer workflows where cost-efficiency is paramount. We utilize a **Risk-Free Metered Billing** structure: you are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data quality is low or the query fails to find a match, the cost is $0.00. This ensures your autonomous agents can explore large datasets without racking up costs for "not found" results.

## Get Your Free B2B Enrichment API Key

Ready to turn your LLM into a data-driven SDR? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and start enriching leads on the free tier today.