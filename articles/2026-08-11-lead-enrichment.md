# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying a Model Context Protocol (MCP) native API server. By integrating the B2B Lead Enrichment MCP server, developers can transform Claude Desktop or Cursor into real-time sales intelligence engines that fetch verified, real-time company profiles and technographic data on-demand.

## Core Features
This MCP server provides a standardized interface for LLMs to query high-fidelity business data, utilizing **Zod-based strict schema definitions** to virtually eliminate parameter hallucinations during tool-calling.

*   **Deep Firmographics:** Access real-time data on employee counts, revenue brackets, industry classification, and headquarters geolocation.
*   **Technographic Intelligence:** Identify the target's underlying tech stack, including CRM usage, cloud providers, and marketing automation tools.
*   **Intent & Growth Signals:** Track hiring trends, recent funding rounds, and expansion markers that indicate a high propensity to buy.
*   **Zero-Hallucination Parameters:** Tools are annotated with strict Zod schemas, ensuring the LLM passes valid domains and company identifiers every time.

## Claude Desktop Configuration
To enable these tools in Claude Desktop, add the following configuration to your `claude_desktop_config.json` file. This tells Claude how to connect to the remote MCP endpoint via an SSE (Server-Sent Events) transport.

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
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Example
When you ask an LLM "Find the tech stack and headcount for stripe.com", the MCP server returns a clean, structured JSON-RPC payload that the model processes immediately:

```json
{
  "tool": "enrich_lead",
  "result": {
    "companyName": "Stripe",
    "domain": "stripe.com",
    "industry": "Financial Services",
    "headcount": "7,000+",
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "hiring_velocity": "High",
      "recent_events": "Expansion into Southeast Asian markets"
    },
    "confidenceScore": 0.98,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing
Traditional B2B data providers charge massive upfront platform fees. This MCP implementation utilizes a **Risk-Free Metered Billing** structure specifically designed for AI agents. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the record is not found, or the query fails to meet the accuracy threshold, the cost is $0. This allows for high-volume SDR swarms and autonomous research agents to operate with high ROI and zero waste.

## Get Your Free API Key
Ready to upgrade your AI's sales intelligence? Visit the link below to generate your API key and start enriching leads natively within Claude, Cursor, or your custom MCP client.

[Get Started at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)