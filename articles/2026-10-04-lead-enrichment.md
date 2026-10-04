# How to Connect Cursor and Claude Desktop to a Live B2B Lead Enrichment MCP API

Connecting your IDE or LLM to live B2B firmographics is best achieved via a native Model Context Protocol (MCP) server, enabling real-time lead enrichment directly within tools like Cursor, VS Code, or Claude Desktop. This architectural pattern eliminates manual data exports and custom middleware by providing a standardized JSON-RPC interface for fetching validated company profiles, technographic stacks, and buyer intent signals natively.

## Core Features
The B2B Lead Enrichment MCP server provides a high-performance bridge between LLM agents and deep organizational data. By utilizing **Zod-annotated schemas**, the server enforces strict type-safety, which virtually eliminates the parameter hallucinations common when LLMs attempt to guess API structures.

*   **Firmographic Intelligence:** Instant access to headcount, revenue, industry classification, and headquarters location.
*   **Technographic Analysis:** Identify the underlying tech stack of any lead, including CRM, cloud providers, and analytics tools.
*   **Real-Time Intent Signals:** Surface active buying signals and industry-specific triggers to prioritize outreach.
*   **Zero-Hallucination Schemas:** Every tool call is governed by a strict JSON schema, ensuring the LLM passes valid, actionable identifiers every time.

## Integration Configuration
To enable these tools in **Claude Desktop** or **Cursor**, add the following configuration to your `claude_desktop_config.json` or your IDE's MCP settings.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "curl",
      "args": [
        "-s",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Standardized JSON-RPC Response
When your agent invokes the `enrich_lead` tool, the MCP server returns a structured payload designed for immediate token-efficient processing by the LLM. Below is an example of the clean response data received:

```json
{
  "method": "tools/call",
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "ExampleCorp",
          "industry": "Enterprise Software",
          "technographics": ["Salesforce", "AWS", "Segment"],
          "intentSignals": "High - Recent expansion in DevOps team",
          "confidenceScore": 0.94,
          "headcount": "501-1000",
          "estimatedRevenue": "$50M-$100M"
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing
Traditional data APIs charge for every request, regardless of the quality of the result. Our MCP server implements a **Risk-Free Metered Billing** model optimized for AI agents. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the confidence score is too low, or the query fails to find a match, the cost is $0. This allows you to build autonomous SDR swarms and data-hungry workflows without the risk of burning through your budget on "null" responses.

## Get Started with Your Free API Key
Ready to upgrade your AI agent with real-time B2B data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching leads directly in your terminal or IDE today.