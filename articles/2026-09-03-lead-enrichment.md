# How to Equip Cursor and VS Code with Real-Time B2B Lead Enrichment via MCP

To give Cursor or VS Code native access to live firmographics and technographics without custom middleware, developers are adopting the Model Context Protocol (MCP) to bridge LLMs with real-time B2B data. This B2B lead enrichment MCP server provides direct access to company profiles and intent signals using a standardized JSON-RPC interface that eliminates manual data entry and LLM parameter hallucinations.

## Core Features

This MCP server acts as a live bridge between your IDE and deep-web B2B intelligence. By implementing the Model Context Protocol, it allows your AI agent to pull context-aware data into your development or sales-automation workflow.

*   **Deep Firmographic Layers:** Retrieve real-time data on employee count, revenue brackets, headquarters location, and industry classification.
*   **Technographic Intelligence:** Identify the target company’s current tech stack, including cloud providers, CRM usage, and frontend frameworks.
*   **Growth & Intent Signals:** Access dynamic indicators such as recent funding rounds, hiring surges, and expansion signals.
*   **Zero Hallucination Guarantee:** Tools are defined with strict **Zod schemas** and descriptive annotations, ensuring the LLM maps parameters like `domain` or `company_name` with 100% accuracy.

## IDE Configuration for Cursor and VS Code

To enable these tools in Cursor or VS Code (via the MCP extension), add the following to your `project.json` or global MCP settings:

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
        "LEAD_ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Example

When you trigger the `enrich_lead` tool through your AI agent, the server returns a structured JSON payload. This clean data allows the LLM to reason about the lead without the noise of unstructured HTML scraping:

```json
{
  "tool": "enrich_lead",
  "parameters": { "domain": "stripe.com" },
  "response": {
    "companyName": "Stripe",
    "industry": "Financial Services",
    "headcount": "7,000+",
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "hiringTrend": "High",
      "recentNews": "Expanding cross-border payment rails in EMEA"
    },
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing

Traditional B2B data providers charge high monthly retainers regardless of data quality. This MCP server utilizes a **Performance-Based Billing** model. You are only charged for successful enrichments that return a **Confidence Score > 0.6**. If the server cannot find high-quality data or returns a low-confidence match, the query cost is exactly $0. This allows you to build autonomous SDR swarms and sales-research agents with a predictable, ROI-positive cost structure.

## Get Started with the B2B Lead Enrichment MCP API

Ready to build smarter sales tools? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly.