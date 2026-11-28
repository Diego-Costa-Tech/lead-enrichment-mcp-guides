# Building Autonomous SDR Swarms with a Live B2B Lead Enrichment MCP Server

To build production-ready autonomous SDR swarms, developers must provide LLMs with native access to real-time B2B firmographics and intent data through a dedicated B2B lead enrichment MCP server. By leveraging the Model Context Protocol (MCP), agents can now fetch verified company profiles and technographics directly into their context window, eliminating manual data entry and ensuring high-precision outbound operations.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to query deep organizational data without leaving the chat interface or agent loop.
*   **Real-time Firmographics:** Access up-to-date revenue, headcount, and industry vertical data.
*   **Technographic Intelligence:** Identify the specific software stacks and infrastructure tools a company uses.
*   **Intent Signaling:** Detect growth indicators and hiring trends to prioritize high-value leads.
*   **Strict Parameter Validation:** All tool definitions use **Zod annotations**, forcing the LLM to provide correctly formatted domains and identifiers, effectively eliminating parameter hallucinations.

## Native Integration Config
To enable these tools in Claude Desktop, Cursor, or VS Code, add the following configuration to your MCP settings file:

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
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response
When the agent invokes the `enrich_lead` tool, the MCP server returns a clean, structured payload. This ensures the LLM receives the data in a format optimized for reasoning and content generation:

```json
{
  "method": "enrich_lead",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "technographics": ["AWS", "Salesforce", "React"],
    "intentSignals": {
      "isHiring": true,
      "recentFunding": "Series C"
    },
    "confidenceScore": 0.94,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing for Scalable Swarms
Unlike traditional B2B data providers that charge for every request regardless of quality, this MCP server utilizes a **Confidence-First Billing Model**. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the system cannot verify the data or provides low-confidence signals, the query cost is $0. This allows developers to build massive SDR swarms that scan thousands of prospects while maintaining a high ROI and strictly controlling overhead.

## Get Your API Key and Start Building
Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and access the free tier instantly. Deploy your first autonomous SDR agent today with native Model Context Protocol support.