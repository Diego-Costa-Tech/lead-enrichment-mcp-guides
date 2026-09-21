# How to Give Cursor and Claude Desktop Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying a Model Context Protocol (MCP) native API server. By integrating the B2B Lead Enrichment MCP server, developers can transform Cursor, VS Code, or Claude Desktop into powerful sales intelligence tools that pull real-time company profiles directly into the AI’s active reasoning context.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to query deep organizational data. By leveraging **Model Context Protocol**, the server exposes tools that allow agents to browse:
*   **Comprehensive Firmographics:** Real-time industry classification, headcount growth, and revenue estimates.
*   **Technographic Layers:** Detection of active software stacks (SaaS, Cloud providers, CRM usage).
*   **High-Intensity Intent Signals:** Tracking organizational shifts that indicate a propensity to purchase.
*   **Hallucination Prevention:** Every tool parameter is defined using **strict Zod annotations**, ensuring the LLM passes correctly formatted domain names and filters, eliminating the common "parameter hallucination" found in traditional REST-to-Agent bridges.

## Configuration for Cursor and Claude Desktop
To enable these tools, add the following configuration to your `claude_desktop_config.json` or your Cursor "External MCP" settings. This connects your environment to the production-ready endpoint.

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
      ]
    }
  }
}
```

## JSON-RPC Enrichment Response Example
When you ask an AI agent to "Enrich the company stripe.com," the MCP server executes the `enrich_lead` tool and returns a structured JSON-RPC response. This clean data allows the LLM to provide factual insights rather than guessing:

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
    "companyName": "Stripe, Inc.",
    "industry": "FinTech / Payments",
    "employeeCount": 8000,
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": ["Global expansion in APAC", "New regulatory compliance hiring"],
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing
Traditional B2B data APIs charge per request, regardless of whether the data is found or accurate. This MCP server utilizes a **Risk-Free Metered Billing** structure specifically designed for autonomous agents. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the record is missing, or the query fails to meet the threshold, the cost is $0. This ensures that scaling SDR swarms or automated research pipelines remains cost-effective and high-signal.

## Get Started with the Free Tier
Equip your AI agents with the same data used by elite sales teams. Visit the link below to generate your API key and start enriching leads with the free tier today.

[Get Your B2B Lead Enrichment MCP Key at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)