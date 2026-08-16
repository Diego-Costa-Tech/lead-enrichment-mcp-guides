# Supercharging Cursor and VS Code with Live B2B Firmographic MCP Tools

To give Cursor or VS Code Copilot native access to real-time B2B firmographics and intent data without building custom middleware, you must implement a Model Context Protocol (MCP) server that exposes a standardized `enrich_lead` tool. This specific B2B Lead Enrichment MCP server allows AI agents to instantly pull company profiles, technographics, and intent signals directly into your coding environment, enabling the rapid development of automated sales workflows and growth engineering scripts.

## Core Features
The B2B Lead Enrichment MCP API transforms your IDE into a powerful sales intelligence engine by providing three distinct layers of data via standardized MCP tools. Every tool is defined with strict **Zod-based schema annotations**, ensuring that the LLM understands the exact data types required and effectively eliminating parameter hallucinations that typically plague unstructured B2B lookups.

*   **Deep Firmographics:** Access validated data points including **verified employee counts**, **revenue brackets**, **HQ locations**, and **industry classifications**.
*   **Technographic Detection:** Identify the target’s software stack, from CRM usage to cloud infrastructure, allowing for highly personalized outbound messaging.
*   **Real-time Intent Signals:** Retrieve data on recent **funding rounds**, **active job postings**, and **news events** that signal a high propensity to buy.
*   **Confidence Scoring:** Every response includes a precision metric to help your autonomous agents decide whether to proceed with an action or flag the lead for human review.

## Configuration for Cursor & VS Code
Integrating this capability into your IDE takes less than 30 seconds. By adding the following configuration to your `project.json` or global MCP settings, your AI agent (Cursor or VS Code Copilot) will automatically discover the `enrich_lead` tool.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Standardized JSON-RPC Response
When your agent invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC object. This ensures that the LLM can parse the technical attributes without guessing the field names or data formats.

```json
{
  "tool_use": "enrich_lead",
  "response": {
    "companyName": "Acme Corp",
    "domain": "acme.ai",
    "industry": "Enterprise Software",
    "headcount": 450,
    "technographics": ["Salesforce", "AWS", "HubSpot", "React"],
    "intentSignals": [
      { "type": "funding", "value": "Series C", "date": "2023-11-12" },
      { "type": "hiring", "role": "DevOps Engineer", "count": 4 }
    ],
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing: Precision Over Volume
Unlike traditional data providers that charge for every API hit regardless of quality, the B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** structure. You are only billed for successful enrichments where the **Confidence Score is > 0.6**. If the server returns low-quality data, an empty profile, or fails to find the target, the cost of that query is $0. This allows developers to build high-volume SDR swarms and lead-generation bots without the risk of burning through budgets on "bad data."

## Get Started with the B2B Lead Enrichment MCP API
Ready to give your local LLM agents the power of live B2B intelligence? Visit the link below to generate your free-tier API key and start enriching leads directly in your terminal or IDE.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to get your free API key now.**