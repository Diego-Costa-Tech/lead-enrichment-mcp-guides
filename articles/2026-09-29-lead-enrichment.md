# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your IDE context. By utilizing the Model Context Protocol (MCP), developers can eliminate manual data entry and context-switching, allowing AI agents to query real-time company profiles and technographic telemetry through a standardized JSON-RPC interface.

## Core Features

The **B2B Lead Enrichment MCP Server** provides a robust suite of tools designed to provide LLMs with high-fidelity business intelligence. Unlike static datasets, this server provides real-time access to multiple data layers:

*   **Firmographic Intelligence:** Retrieve deep company metadata including employee headcount, revenue brackets, industry NAICS codes, and headquarters geolocation.
*   **Technographic Stack Mapping:** Identify the underlying software stack of a target company, from CRM usage to cloud infrastructure, enabling precise competitive analysis.
*   **Intent Signal Processing:** Access real-time behavioral signals that indicate a company's current purchasing trajectory or hiring expansion.
*   **Schema-Strict Parameters:** All tool inputs are defined using **Zod annotations**, forcing the LLM to provide valid domain names and preventing the "hallucinated parameter" issue common in generic API calls.

## Configuration for Cursor and Claude Desktop

To integrate these tools, add the following configuration to your `cursor.json` or `claude_desktop_config.json`. This points your agent to the production MCP endpoint:

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
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example

When the `enrich_lead` tool is invoked, the MCP server returns a structured payload. This deterministic output allows the LLM to parse specific data points for use in code generation, email drafting, or lead scoring logic:

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": { "domain": "stripe.com" }
  },
  "result": {
    "companyName": "Stripe, Inc.",
    "industry": "Fintech / Payments",
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "hiring_growth": "high",
      "funding_status": "Series I",
      "expansion_keywords": ["Global Payments", "Tax Automation"]
    },
    "confidenceScore": 0.98
  }
}
```

## The Value Proposition: Risk-Free Metered Billing

Traditional B2B data providers demand heavy upfront annual contracts. This MCP-native server operates on a **Risk-Free Metered Billing** structure specifically designed for AI agent workflows. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server returns low-quality data or fails to find a match, the query cost is $0. This allows you to scale autonomous SDR swarms and automated research agents without the risk of burning credits on "Not Found" responses.

## Get Started with a Free API Key

Ready to bridge the gap between your LLM and real-world B2B data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching your AI workflows today.