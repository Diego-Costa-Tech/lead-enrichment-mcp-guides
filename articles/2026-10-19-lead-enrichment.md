# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

Integrating Claude Desktop with a native B2B lead enrichment MCP server is the most efficient way to provide LLMs with real-time firmographic and intent data without building custom middleware. By leveraging the Model Context Protocol, developers can grant AI agents the ability to autonomously query company profiles, technographics, and contact intelligence directly within their chat interface or IDE.

## Core Features
The B2B Lead Enrichment MCP API provides a comprehensive data layer designed specifically for LLM tool-calling. To ensure high reliability and prevent parameter hallucinations common in agentic workflows, all tool definitions utilize **strict Zod schema annotations**.

*   **Deep Firmographics:** Access real-time data on company size, revenue, industry classification, and headquarters location.
*   **Technographic Intelligence:** Identify the software stack of a target lead, including CRM, cloud providers, and marketing automation tools.
*   **Intent Signals:** Track recent funding rounds, hiring trends, and expansion news that signal a high propensity to buy.
*   **Hallucination Prevention:** Every tool, such as `enrich_lead` and `search_companies`, uses rigorous JSON-RPC validation to ensure the LLM passes correctly formatted domain names and professional emails.

## Claude Desktop Configuration
To enable these tools in Claude Desktop, add the following configuration to your `claude_desktop_config.json` file (typically found in `~/Library/Application Support/Claude/` on macOS).

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response
When Claude calls the `enrich_lead` tool, the MCP server returns a clean, structured payload. This allows the model to process the data immediately without needing to parse unstructured HTML or messy CSV exports.

```json
{
  "result": {
    "companyName": "Stripe",
    "industry": "Fintech / Payments",
    "employeeCount": 7000,
    "technographics": ["AWS", "React", "Salesforce", "Marketo"],
    "intentSignals": [
      {
        "type": "hiring_surge",
        "details": "Increasing headcount in Enterprise Sales by 15%."
      }
    ],
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing
Unlike traditional B2B data providers that charge per seat or for failed queries, this MCP server utilizes a performance-based **Risk-Free Metered Billing** model. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the database cannot find a match or the data quality is low, the query costs $0, making it the most cost-effective solution for building autonomous SDR swarms and bulk enrichment pipelines.

## Get Your Free B2B Enrichment API Key
Ready to upgrade your AI agents with real-world intelligence? Visit the portal to claim your free tier API key and start enriching leads natively within Claude, Cursor, or your custom MCP client.

[Visit lead-enrichment-mcp.agent-infra.workers.dev to get started](https://lead-enrichment-mcp.agent-infra.workers.dev)