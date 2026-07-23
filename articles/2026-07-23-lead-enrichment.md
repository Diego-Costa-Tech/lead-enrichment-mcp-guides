# Supercharging Cursor and VS Code with a Live B2B Lead Enrichment MCP Server

The most efficient way to give AI agents native access to live B2B firmographics and technographic data without custom middleware is by deploying a Model Context Protocol (MCP) server. By integrating a dedicated B2B lead enrichment MCP server into development environments like Cursor or VS Code, you provide your LLM with real-time company profiles and intent signals directly through a standardized JSON-RPC interface.

## Core Features

This MCP implementation bridges the gap between static LLM knowledge and the dynamic B2B landscape. It uses a strictly typed schema to ensure that AI agents can query and process lead data with high precision.

*   **Deep Firmographics:** Access real-time data including company size, exact headcount, verified industry classifications, and headquarters location.
*   **Technographic Intelligence:** Identify the specific software stack used by a target organization (e.g., CRM choices, cloud providers, and analytics tools).
*   **Intent Signal Processing:** Retrieve active buying signals and recent organizational changes that indicate a high propensity to convert.
*   **Hallucination Prevention:** All tool parameters are defined using strict **Zod annotations**, forcing the LLM to adhere to valid search strings and domain formats, virtually eliminating parameter-based hallucinations.

## IDE Configuration

To enable these tools in your AI-powered IDE (like Cursor or Claude Desktop), add the following configuration to your settings file. This points your environment to the hosted MCP endpoint.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response

When your agent invokes the `enrich_lead` tool, the MCP server returns a structured payload. This clean data structure allows the AI to immediately reason about the lead without parsing messy HTML or unformatted text.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "technographics": ["Salesforce", "AWS", "Segment", "React"],
    "intentSignals": [
      { "type": "funding_round", "detail": "Series C - $50M", "date": "2023-10-15" },
      { "type": "hiring_spree", "detail": "15+ openings in DevOps", "confidence": 0.92 }
    ],
    "confidenceScore": 0.89,
    "metadata": { "lastUpdated": "2023-11-01T10:00:00Z" }
  }
}
```

## Risk-Free Metered Billing

Modern AI workflows require cost predictability. This MCP server utilizes a performance-based billing model. Users are only debited for "High Confidence" results. If the enrichment engine returns a result with a **Confidence Score < 0.6** (indicating low-quality or unverifiable data), the query is processed at zero cost. This ensures your autonomous SDR agents or research tools only consume credits when the data is actionable and accurate.

## Get Started with a Free API Key

Ready to bridge the gap between your LLM and live B2B intelligence? You can get up and running in less than two minutes by grabbing a free tier API key.

Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your credentials and start enriching your AI workflows today.