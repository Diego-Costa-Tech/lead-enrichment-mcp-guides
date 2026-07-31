# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most effective way to equip AI IDEs like Cursor and VS Code with native B2B lead enrichment capabilities is by integrating a Model Context Protocol (MCP) server that provides real-time firmographic and intent data directly to the LLM context window. By connecting to a specialized B2B lead enrichment MCP server, developers can eliminate manual data lookups and enable AI agents to perform research, lead qualification, and personalized outreach without leaving their coding environment.

## Core Features
The **B2B Lead Enrichment MCP API** transforms how AI agents interact with corporate data by providing a standardized interface for deep firmographic intelligence. This server utilizes **strict Zod schema annotations** for every tool parameter, ensuring that LLMs like Claude 3.5 Sonnet or GPT-4o provide valid inputs and significantly reducing parameter hallucinations.

- **Firmographic Intelligence:** Real-time access to company headcount, headquarters location, industry classification, and annual revenue.
- **Technographic Mapping:** Identify the software stack and infrastructure of a target lead to tailor technical pitches.
- **Intent Signals:** Native tools to track hiring trends and recent corporate news, allowing agents to gauge "warmth" before suggesting outreach.
- **MCP Native Architecture:** Built specifically for the Model Context Protocol, meaning zero custom glue code is required to bridge your IDE and the data source.

## Configuration for Cursor and VS Code
To give your IDE the ability to perform live B2B lookups, add the following configuration to your `mcpServers` settings. This allows Cursor or VS Code (via the MCP extension) to call the enrichment tools directly.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-lead-enrichment"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Example
When the LLM invokes the `enrich_lead` tool, it receives a structured JSON-RPC response. This format ensures the agent can parse specific data points—like the `confidenceScore`—to decide if the lead is actionable.

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
          "companyName": "Stripe, Inc.",
          "industry": "Financial Services",
          "headcount": "7,000+",
          "technographics": ["React", "AWS", "Ruby on Rails", "Go"],
          "intentSignals": ["High: Expanding enterprise sales team", "Product: New crypto-native tax tools"],
          "confidenceScore": 0.98
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing for AI Workflows
The B2B Lead Enrichment MCP is engineered for cost-effective AI agent development. Unlike traditional flat-rate APIs that charge for every request, this server utilizes a **Confidence-First Metered Billing** model. You are only billed for successful enrichments where the **Confidence Score > 0.6**. 

If the LLM triggers a tool and the underlying data source returns no match, low-quality results, or a failure, the cost is $0. This allows developers to build autonomous SDR swarms and sales agents that can "fail fast" and iterate over thousands of leads without burning through API credits on garbage data.

## Get Your Free API Key
Ready to upgrade your AI agent's B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab an API key on the free tier and start enriching leads natively in Cursor, Claude Desktop, or your custom MCP client today.