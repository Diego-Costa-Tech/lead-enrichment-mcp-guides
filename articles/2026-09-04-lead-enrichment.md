# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools

Integrating a Model Context Protocol (MCP) server directly into your IDE allows your AI agent to access live B2B firmographics and intent data without writing custom API middleware. This setup enables Cursor or VS Code Copilot to perform real-time lead enrichment, company profiling, and sales intelligence tasks using a standardized, low-latency B2B lead enrichment MCP server.

## Core Features
The B2B Lead Enrichment MCP API provides a robust layer of intelligence for autonomous agents. By utilizing strict **Zod-based schema definitions**, the server ensures that LLM parameter hallucinations are eliminated, forcing the model to provide valid email domains or LinkedIn URLs before execution.

*   **Deep Firmographics:** Access real-time data including employee count, estimated revenue, industry classification, and headquarters location.
*   **Technographic Intelligence:** Identify the target's current tech stack, from cloud providers (AWS, GCP) to specific SaaS tools like Salesforce or HubSpot.
*   **Intent & Signals:** Retrieve recent growth indicators, hiring trends, and funding news to prioritize high-value accounts.
*   **Hallucination Protection:** Every tool parameter is strictly typed, ensuring the LLM passes validated strings rather than "guessing" data points.

## IDE Configuration
To enable these tools in **Cursor** or **Claude Desktop**, add the following configuration to your settings file. This points the Model Context Protocol client to our hosted endpoint.

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
        "ENRICHMENT_API_KEY": "YOUR_SECRET_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
When the LLM calls the `enrich_lead` tool, it receives a structured JSON-RPC response. This data is injected directly into the conversation context, allowing the agent to reason about the company immediately.

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
    "companyName": "Stripe",
    "industry": "Financial Services",
    "headcount": "7000+",
    "technographics": ["React", "Ruby on Rails", "AWS", "Salesforce"],
    "intentSignals": {
      "hiring": "High",
      "recentNews": "Expansion into Southeast Asia"
    },
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing
Unlike traditional B2B data providers that charge for every API call regardless of result quality, this MCP server utilizes a **performance-first billing model**. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the record is not found, or the confidence score is low, the query cost is $0. This allows developers to build high-volume SDR swarms and autonomous agents without the risk of burning budget on "not found" errors or hallucinated data.

## Get Started for Free
Ready to empower your AI agents with live B2B data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and start using the free tier today.