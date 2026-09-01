# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your IDE. By connecting Cursor or VS Code to a dedicated B2B lead enrichment MCP server, developers can eliminate parameter hallucinations and provide AI agents with real-time company profiles and technographic data.

## Core Features

This MCP implementation provides a standardized interface for LLMs to interact with deep market intelligence. By leveraging the **Model Context Protocol**, the server enforces strict data structures that ensure high-fidelity retrieval:

*   **Real-Time Firmographics:** Access up-to-date **company revenue, employee counts, industry classifications, and headquarters locations** directly within the chat context.
*   **Deep Technographics:** Identify the specific **software stacks, cloud providers, and specialized tools** a target company is currently using to tailor code or outreach.
*   **Intent & Signal Detection:** Query for **recent funding rounds, active job openings, and product launches** to trigger automated workflows based on high-intent events.
*   **Zero-Hallucination Parameters:** Every tool definition uses **strict Zod annotations**, forcing the LLM to provide valid domains or company names, drastically reducing the "hallucination rate" common in standard API calls.

## IDE Configuration

To enable these tools in **Cursor**, **VS Code Copilot**, or **Claude Desktop**, add the following configuration to your settings file. This points the LLM to the hosted MCP endpoint, allowing it to discover the `enrich_lead` and `get_company_intent` tools automatically.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Example

When your AI agent invokes the `enrich_lead` tool, it receives a structured JSON-RPC response. This clean data allows the LLM to reason about a prospect with 100% accuracy rather than guessing details from its training data.

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
          "technographics": ["AWS", "React", "Ruby on Rails", "Kubernetes"],
          "intentSignals": "High (Active hiring for Enterprise Sales)",
          "revenueRange": "$1B+",
          "headcount": 7000,
          "confidenceScore": 0.98
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing

Modern AI infrastructure should be cost-effective. This MCP server utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the data is low quality, the match is ambiguous, or the query fails, the cost is exactly $0. This allows you to build autonomous SDR swarms and bulk enrichment pipelines without worrying about paying for "no-results" or hallucinated data points.

## Get Started with a Free API Key

Ready to upgrade your AI agent's intelligence? Visit the link below to generate your API key and start querying live B2B data via MCP today.

[Get Your Free B2B Enrichment API Key](https://lead-enrichment-mcp.agent-infra.workers.dev)