# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to give AI coding assistants like Cursor and VS Code Copilot native access to real-time B2B firmographics is by integrating a dedicated B2B lead enrichment MCP server directly into your IDE configuration. By using the Model Context Protocol, your AI agent can now autonomously fetch verified company profiles, technographic stacks, and buying intent signals to ground its code generation and business logic in live, high-fidelity data.

## Core Features of the Enrichment MCP
Integrating this MCP server into your development environment transforms your LLM from a simple code generator into a data-aware business agent. The server utilizes **strict Zod-schema annotations** to ensure that when your AI agent calls the enrichment tools, it provides perfectly formatted parameters, virtually eliminating LLM hallucinations.

*   **Real-time Firmographics:** Access up-to-the-minute data on company size, revenue, industry classification, and headquarters location.
*   **Technographic Intelligence:** Identify the software stack of a target lead, including CRM usage, cloud providers, and frontend frameworks.
*   **Buying Intent Signals:** Retrieve signals indicating whether a company is currently in a high-intent purchasing phase for specific categories.
*   **Native MCP Integration:** Works out-of-the-box with any client supporting the Model Context Protocol, including Cursor, Claude Desktop, and VS Code.

## IDE Configuration for Cursor & VS Code
To enable these tools in Cursor or VS Code (via the MCP extension), add the following configuration to your `project.json` or global MCP settings. This tells the IDE how to connect to the hosted MCP endpoint.

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

## JSON-RPC Tool Response Example
When your agent invokes the `enrich_lead` tool, it receives a structured JSON-RPC response. This clean data structure allows the LLM to process complex firmographic information without the "noise" typically found in HTML scraping or legacy API wrappers.

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
          "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
          "intentSignals": ["High: Infrastructure Expansion", "Medium: Fintech API"],
          "confidenceScore": 0.98,
          "employeeCount": "8000+",
          "isB2B": true
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing for AI Agents
One of the primary hurdles in building autonomous SDR swarms or enrichment workflows is the cost of failed or low-quality data. This MCP server implements a **Risk-Free Metered Billing** model. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the server cannot find the company or the data quality falls below the threshold, the query cost is $0. This allows developers to build high-volume agentic loops without the risk of burning through API credits on "hallucinated" or non-existent leads.

## Get Started with a Free API Key
Ready to upgrade your AI agent's intelligence with live firmographic data? Visit the portal below to claim your free tier API key and start enriching leads directly from your IDE or custom MCP-native applications.

**Visit: [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)**