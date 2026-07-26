# Supercharging Cursor and VS Code with Real-Time B2B Lead Enrichment via MCP

To give your AI coding assistant native access to real-time B2B firmographics and intent data without custom middleware, you must deploy a Model Context Protocol (MCP) server. By connecting Cursor or VS Code to a specialized B2B lead enrichment MCP server, you enable LLMs to perform live lookups of company profiles, technographics, and buying signals directly within your IDE development environment.

## Core Features

The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to ingest deep organizational intelligence. By leveraging the Model Context Protocol, the server exposes tools that handle complex data retrieval, ensuring your AI agents have the context needed for personalized outreach or market analysis.

*   **Deep Firmographics:** Access real-time data on company size, revenue, industry classification (SIC/NAICS), and headquarters location.
*   **Technographic Stack Mapping:** Identify the specific software and infrastructure used by a target organization (e.g., "Uses AWS, Salesforce, and React").
*   **Intent Signal Detection:** Pull recent funding rounds, hiring trends, and expansion news to identify high-intent accounts.
*   **Schema-Validated Tools:** Every tool uses strict **Zod annotations**, forcing the LLM to provide syntactically correct inputs (like valid domain names) and significantly reducing parameter hallucinations common in unstructured API calls.

## Configuration for Cursor and VS Code

To integrate this capability into your AI-assisted workflow, add the following configuration to your MCP settings. For Cursor, navigate to **Settings > Models > MCP** and add a new server with the following details:

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example

When you ask Cursor, "Analyze the technographics for stripe.com," the MCP server executes the `enrich_lead` tool and returns a structured JSON-RPC response that the LLM injects directly into its context window:

```json
{
  "tool": "enrich_lead",
  "parameters": { "domain": "stripe.com" },
  "response": {
    "companyName": "Stripe, Inc.",
    "industry": "Financial Services",
    "technographics": ["AWS", "Kubernetes", "Ruby", "React", "Salesforce"],
    "intentSignals": [
      { "type": "Expansion", "score": 0.85, "summary": "Recent hiring surge in EMEA region" }
    ],
    "firmographics": {
      "employees": "7,000+",
      "estimatedRevenue": "$14B+",
      "hq": "South San Francisco, CA"
    },
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing

Traditional B2B data providers charge high flat fees regardless of data quality. This MCP server utilizes a **Confidence-First Metered Billing** model. Your account is only debited for enrichments where the **Confidence Score > 0.6**. If the server returns a low-confidence result, or if no verified data is found, the query cost is $0. This allows developers to build high-scale autonomous SDR swarms and SDR agents without the risk of burning budget on "not found" or "hallucinated" data.

## Get Started with Your Free API Key

Ready to turn your LLM into a powerful sales intelligence engine? Visit the portal to generate your API key and access the free tier instantly.

[Get Your API Key at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)