# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

Integrating live B2B firmographics and intent data into LLMs is most effectively achieved by deploying a Model Context Protocol (MCP) server that provides direct tool-calling capabilities to the model. By connecting Claude Desktop or Cursor to a B2B lead enrichment MCP server, developers can eliminate custom middleware and give agents real-time access to validated company profiles and technographic data with zero latency.

## Core Features
The B2B Lead Enrichment MCP API utilizes a strictly typed architecture to ensure high-fidelity data retrieval for AI agents. By implementing **Zod-based schema validation** for all tool parameters, the server virtually eliminates LLM hallucinations during the argument-generation phase. Key data layers provided include:

*   **Firmographic Intelligence:** Real-time lookup of company size, revenue brackets, industry classification (NAICS/SIC), and headquarters location.
*   **Technographic Stack:** Identification of current software deployments (e.g., CRM, Cloud Provider, Analytics tools) to help agents tailor sales pitches.
*   **Intent & Signal Tracking:** Active monitoring of growth signals, funding rounds, and hiring trends that indicate high-propensity leads.
*   **Structured Tooling:** The `enrich_lead` tool is optimized for the Model Context Protocol, allowing Claude to interpret complex B2B datasets as native context.

## Installation & Configuration
To enable these tools in Claude Desktop, add the following configuration to your `claude_desktop_config.json` file. This setup uses the production MCP endpoint to bridge your local agent with the live lead enrichment engine.

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
When the LLM invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This allows the agent to reason over the data points without parsing messy HTML or unstructured text.

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": { "domain": "stripe.com" }
  },
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Stripe, Inc.",
          "industry": "Financial Services",
          "technographics": ["AWS", "React", "Salesforce", "Zendesk"],
          "intentSignals": ["High: Expanding EMEA operations", "Recent Series I funding"],
          "confidenceScore": 0.98,
          "estimatedRevenue": "$1B+",
          "employeeCount": "7,000+"
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing
Traditional B2B data providers charge heavy upfront credits regardless of data quality. This MCP server introduces a developer-first **Risk-Free Metered Billing** model. The system calculates a `confidenceScore` for every enrichment; you are only billed for successful queries where the score exceeds 0.6. If the data is low-quality, outdated, or not found, the query cost is exactly $0, making it the most cost-effective solution for building autonomous SDR swarms and high-volume sales agents.

## Get Your Free B2B Enrichment API Key
Ready to upgrade your AI agent with real-time B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start enriching leads on the free tier today.