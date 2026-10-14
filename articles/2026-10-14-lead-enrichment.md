# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

Integrating Claude Desktop or Cursor with real-time B2B lead enrichment data is most effectively achieved by deploying a native Model Context Protocol (MCP) server. This architecture allows LLMs to autonomously query high-fidelity firmographic and intent data using strict JSON-RPC schemas, eliminating the need for manual data lookups or fragile custom middleware.

## Core Features of the B2B Enrichment MCP

The B2B Lead Enrichment MCP server provides a standardized interface for AI agents to retrieve deep intelligence on companies and prospects. By leveraging **Zod-validated parameter schemas**, the server effectively eliminates LLM hallucinations during tool calls, ensuring that the model provides valid search queries for every enrichment request.

*   **Firmographic Intelligence:** Retrieve real-time data on company revenue, headcount, industry classification, and headquarters location.
*   **Technographic Data:** Identify the underlying tech stack of a target lead, including CRM usage, cloud providers, and marketing automation tools.
*   **Intent Signals:** Access live signals such as recent funding rounds, executive leadership changes, and hiring trends to prioritize outreach.
*   **Hallucination-Resistant Tooling:** Every tool within this MCP server uses strict type definitions, forcing the LLM to adhere to the required data formats for `enrich_lead` and `search_companies` functions.

## Implementation: Claude Desktop Configuration

To give Claude Desktop native access to this live B2B data, add the following configuration to your `claude_desktop_config.json` file. This connects the client directly to the hosted MCP endpoint.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Payload

When Claude or Cursor invokes the `enrich_lead` tool, the MCP server returns a structured response. This clean data format allows the LLM to synthesize high-quality sales copy or account research instantly.

```json
{
  "tool": "enrich_lead",
  "parameters": { "domain": "stripe.com" },
  "response": {
    "companyName": "Stripe, Inc.",
    "industry": "Financial Services",
    "headcount": "7,000+",
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "recentFunding": "Series I",
      "hiringVelocity": "High",
      "focusArea": "Global Payments Infrastructure"
    },
    "confidenceScore": 0.98,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing for AI Agents

Scaling an AI-driven SDR swarm or an automated research agent requires a predictable cost structure. This MCP server implements a **Success-Only Billing** model. You are only billed for enrichment queries that return a **Confidence Score > 0.6**. If the data is low-quality, the prospect is not found, or the confidence threshold is not met, the query cost is $0. This allows developers to build high-volume workflows without the risk of paying for "I'm sorry, I couldn't find that information" responses.

## Get Your Free B2B Enrichment API Key

Ready to turn your LLM into a high-performance sales researcher? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and start enriching leads on the free tier today.