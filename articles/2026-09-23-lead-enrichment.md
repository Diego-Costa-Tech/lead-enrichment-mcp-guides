# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Integrating real-time company data into IDEs like Cursor and VS Code is best achieved using a Model Context Protocol (MCP) server for B2B lead enrichment. This architecture allows AI agents to fetch live firmographics, technographic stacks, and buyer intent signals directly within the development environment, eliminating manual data entry and preventing LLM context drift during agentic workflows.

## Core Features
The B2B Lead Enrichment MCP server provides deep-link access to several critical data layers designed for AI consumption. By utilizing strict **Zod schema definitions** for tool parameters, the server eliminates common LLM hallucinations when agents attempt to guess company attributes.

*   **Firmographic Intelligence:** Real-time access to company size, revenue brackets, industry classification, and headquarters location.
*   **Technographic Detection:** Identification of a prospect's current software stack, including CRM, cloud providers, and frontend frameworks.
*   **Intent & Signal Analysis:** Live tracking of hiring trends, recent news events, and expansion signals to prioritize outreach.
*   **Zod-Validated Inputs:** Every query is strictly typed, ensuring the LLM passes valid domains and entity names, resulting in higher execution reliability for autonomous agents.

## Cursor and VS Code Configuration
To enable these tools in Cursor or any VS Code environment supporting MCP, add the following configuration to your `project.json` or global MCP settings. This connects your local agent to the live enrichment endpoint.

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
        "LEAD_ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
When your AI agent calls the `enrich_lead` tool, it receives a clean, structured JSON-RPC payload. This format is optimized for LLM "reasoning" steps, allowing the agent to decide the next best action based on the `confidenceScore`.

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": {
      "domain": "stripe.com"
    }
  },
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Stripe",
          "industry": "Fintech / Payments",
          "technographics": ["AWS", "React", "Ruby", "Salesforce"],
          "intentSignals": ["High Hiring Activity", "New Market Expansion"],
          "confidenceScore": 0.98,
          "estimatedRevenue": "Billion+"
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing
Most B2B data providers charge for every API call, regardless of quality. This MCP server implements a **Confidence-First Billing** model. Your account is only debited for successful enrichments that return a Confidence Score > 0.6. If the data is low-quality, the record is missing, or the confidence is low, the query cost is $0. This allows developers to build high-volume SDR swarms and autonomous agents without the risk of burning through budgets on "hallucinated" or empty data points.

## Get Started with a Free API Key
Ready to upgrade your AI agent's firmographic capabilities? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on our free tier and start enriching leads natively within Claude Desktop, Cursor, and VS Code.