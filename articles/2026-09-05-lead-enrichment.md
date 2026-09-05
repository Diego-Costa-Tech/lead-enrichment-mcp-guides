# How to Connect Cursor and Claude Desktop to a Live B2B Lead Enrichment MCP API

Giving LLMs like Claude 3.5 Sonnet native access to live firmographic data and intent signals is most effectively achieved by connecting your IDE or desktop client to a B2B lead enrichment MCP server. By using the Model Context Protocol (MCP), developers can eliminate manual data entry and RAG pipeline overhead, allowing AI agents to query real-time company profiles directly through standardized JSON-RPC tool calls.

## Core Features
The B2B Lead Enrichment MCP API provides a comprehensive data layer designed for high-precision autonomous agents. By utilizing strict **Zod-annotated schemas**, the server effectively eliminates LLM parameter hallucinations, ensuring that the model only provides valid queries for enrichment.

*   **Firmographic Intelligence:** Deep metadata including headcount, revenue range, industry classification, and headquarters location.
*   **Technographic Stack Tracking:** Real-time detection of a company's software stack (e.g., CRM usage, cloud providers, analytics tools).
*   **Intent Signal Identification:** Aggregated signals indicating a company's current buying stage or organizational changes.
*   **Structured Tool-Calling:** Every tool—such as `enrich_lead` and `search_companies`—is defined with explicit property descriptions to guide the LLM's reasoning engine.

## Configuration for Cursor and Claude Desktop
To give your AI agent access to these live data tools, add the following configuration to your `claude_desktop_config.json` or your Cursor "Models" settings.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-lead-enrichment",
        "--api-url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Payload
When the LLM invokes the `enrich_lead` tool, it receives a clean, structured JSON object. This allows the model to reason over the data without parsing messy HTML or unstructured text.

```json
{
  "status": "success",
  "data": {
    "companyName": "Acme Corp",
    "domain": "acme.com",
    "industry": "Enterprise Software",
    "employeeCount": 1250,
    "technographics": ["Salesforce", "AWS", "Segment", "HubSpot"],
    "intentSignals": {
      "hiringTrend": "high",
      "techExpansion": true
    },
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing for Production Workflows
Building cost-effective AI SDR swarms requires predictable unit economics. This MCP server implements a **Confidence-First Billing Model**: your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. Queries that yield low-quality data or "not found" results incur a $0 cost, allowing developers to scale autonomous research workflows without the risk of paying for hallucinated or empty data sets.

## Get Started with the B2B Lead Enrichment MCP
Ready to upgrade your AI agents with real-time firmographic tools? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly.