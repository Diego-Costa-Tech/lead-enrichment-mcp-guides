# How to Give Cursor and VS Code Copilot Live B2B Lead Enrichment Tools via MCP

To eliminate the manual research phase in B2B development and sales engineering workflows, you can integrate a dedicated B2B lead enrichment MCP server directly into your IDE. This implementation allows Cursor and VS Code AI agents to fetch real-time firmographics and intent data natively using the Model Context Protocol, bypassing the need for fragile scraper scripts or manual API wrappers.

## Core Features

The **B2B Lead Enrichment MCP API** provides a standardized interface for LLMs to query deep-layer organizational data. By using this server, your AI agents gain access to:

*   **Real-Time Firmographics:** Instant retrieval of company size, revenue brackets, industry classification, and headquarters location.
*   **Deep Technographics:** Identification of a prospect's current tech stack, including CRM usage, cloud providers, and frontend frameworks.
*   **Native Intent Signals:** Actionable data points such as recent funding rounds, hiring surges, or specific technology migrations.
*   **Zero-Hallucination Parameters:** All tool inputs and outputs are governed by strict **Zod annotations**, ensuring that Claude or GPT-4o never "invents" company data and strictly follows the JSON-RPC schema.

## IDE Configuration (Cursor & VS Code)

To equip your AI editor with these tools, add the following configuration to your `project.json` or the global MCP settings within Cursor:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y", 
        "@modelcontextprotocol/server-http-bridge", 
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "B2B_ENRICH_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Standardized JSON-RPC Response

When your agent triggers the `enrich_lead` tool, the MCP server returns a clean, structured payload. This allows the LLM to process the data for lead scoring, personalized outreach, or account mapping without parsing unstructured HTML or PDFs.

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": {
      "domain": "airbnb.com"
    }
  },
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Airbnb",
          "industry": "Hospitality/Tech",
          "headcount": "5000-10000",
          "technographics": ["Next.js", "Ruby", "AWS", "Salesforce"],
          "intentSignals": ["Increasing focus on AI-driven search"],
          "confidenceScore": 0.94
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing

This MCP server is built for cost-efficiency in autonomous SDR swarms. Unlike traditional data providers that charge per query regardless of quality, this API utilizes a **Confidence-Gated Billing** model. 

You are only billed for successful enrichments where the **Confidence Score is > 0.6**. If the server returns a low-confidence result or fails to find the entity, the request is processed at zero cost ($0), allowing you to scale your AI research agents without the risk of burning credits on "Not Found" responses.

## Get Your Free API Key Today

Ready to give your AI agents the data they need to close deals? Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to grab your API key on the free tier and start enriching leads directly within Claude Desktop, Cursor, or your custom MCP client.