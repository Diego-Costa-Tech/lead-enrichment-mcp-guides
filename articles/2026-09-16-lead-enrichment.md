# How to Give Cursor and VS Code Copilot Live B2B Lead Enrichment Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying a Model Context Protocol (MCP) native server. By integrating the B2B lead enrichment MCP server into your local environment, you enable tools like Cursor, VS Code, and Claude Desktop to execute real-time company profile lookups and intent analysis using standardized JSON-RPC 2.0 calls.

## Core Features
This MCP server exposes a high-fidelity data layer designed specifically for autonomous agents. To prevent the common "parameter hallucination" problem where LLMs guess company details, every tool definition utilizes **strict Zod schema annotations**. This ensures that the model provides correctly formatted domains and identifiers before the request ever hits the API.

*   **Firmographic Intelligence:** Deep-dive into company size, revenue, headquarters, and industry verticalization.
*   **Technographic Stack Mapping:** Identify the underlying technologies (e.g., CRM, Cloud Provider, Analytics) used by a target lead.
*   **Live Intent Signals:** Surface real-time signals that indicate a lead is in an active buying cycle.
*   **Schema-First Design:** Full compliance with the Model Context Protocol specification for seamless tool-calling in any MCP-compatible client.

## Configuring Cursor and Claude Desktop
To give your AI agent access to these tools, add the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings:

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
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## Real-Time JSON-RPC Response Example
When you ask an agent, "Enrich the domain 'stripe.com' and find their current intent signals," the MCP server returns a structured payload that the LLM consumes to provide factual answers:

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "toolResult": {
      "companyName": "Stripe, Inc.",
      "industry": "Financial Services",
      "technographics": ["AWS", "React", "Node.js", "Salesforce"],
      "intentSignals": [
        { "signal": "Expansion into EMEA", "confidence": 0.89 },
        { "signal": "Increased hiring in DevOps", "confidence": 0.72 }
      ],
      "firmographics": {
        "employeeCount": "7000+",
        "estimatedRevenue": "$14B+",
        "headquarters": "South San Francisco, CA"
      },
      "confidenceScore": 0.98
    }
  }
}
```

## Risk-Free Metered Billing
Traditional data APIs charge for every request, regardless of whether the data is useful. This MCP server utilizes a **performance-first billing model**. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server returns low-quality data or fails to find the entity, the query costs $0. This allows developers to build autonomous SDR swarms and sales agents that can scan thousands of leads without the risk of massive bills for "no-match" results.

## Get Your Free API Key Today
Ready to empower your AI agents with live B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on our free tier and start enriching leads directly from your terminal or IDE.