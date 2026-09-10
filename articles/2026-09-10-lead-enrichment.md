# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

To equip AI coding assistants with high-fidelity company intelligence, developers are now leveraging the Model Context Protocol (MCP) to connect a B2B lead enrichment MCP server directly to their IDE environments. This integration provides Cursor and VS Code Copilot with native access to real-time company profiles, technographics, and intent signals, enabling agents to generate context-aware code and sales automation workflows without manual data lookups.

## Core Features of the Lead Enrichment MCP Server

Integrating the B2B Lead Enrichment MCP API into your development environment transforms your LLM from a code generator into a data-aware agent. By using the **Model Context Protocol**, the server exposes tools that allow Cursor or VS Code to fetch deep intelligence on-demand.

*   **Firmographic Intelligence:** Retrieve precise company size, revenue brackets, industry classifications, and headquarters locations.
*   **Technographic Stack Mapping:** Identify the underlying technology stack of a target lead (e.g., Cloud providers, CRM usage, analytics tools).
*   **Real-Time Intent Signals:** Access live data points indicating a company's current buying signals or recent organizational shifts.
*   **Zero-Hallucination Schemas:** All tool parameters are defined using strict **Zod annotations**, ensuring that the LLM provides valid inputs and understands the exact structure of the B2B data requested.

## Configuring Cursor or VS Code for B2B Enrichment

To enable these tools in your IDE, add the following configuration to your MCP settings. This connects your environment to the production-grade worker endpoint.

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

## JSON-RPC Enrichment Response Example

When you ask your agent to "Enrich this domain: stripe.com", the MCP server executes the `enrich_lead` tool and returns a structured JSON-RPC response. This clean data structure prevents the LLM from hallucinating company details.

```json
{
  "tool": "enrich_lead",
  "response": {
    "companyName": "Stripe, Inc.",
    "industry": "Financial Services / Fintech",
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "hiringTrend": "High",
      "expansionSignal": "New market entry in SE Asia"
    },
    "confidenceScore": 0.98,
    "lastUpdated": "2023-10-27T14:30:00Z"
  }
}
```

## Risk-Free Metered Billing for Scalable AI Workflows

One of the most significant barriers to building autonomous SDR swarms is the cost of low-quality data. Our B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** model. Unlike traditional APIs that charge per request regardless of outcome, you are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data is low quality, or if the server returns a "not found" status, your cost is exactly $0, making it the most cost-effective solution for high-volume AI agent workflows.

## Get Started with a Free API Key

Ready to bridge the gap between your AI agent and live B2B intelligence? You can start building today with our free tier.

Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to grab your API key and access the full MCP documentation.