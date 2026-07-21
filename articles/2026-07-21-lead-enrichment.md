# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Integrating a Model Context Protocol (MCP) server for real-time B2B lead enrichment allows IDE-based LLMs like Cursor and VS Code Copilot to access live company profiles and intent data natively. This architecture leverages a standardized B2B lead enrichment MCP server to bridge the gap between static development environments and dynamic firmographic intelligence without requiring custom middleware.

## Core Features

By connecting your development environment to a dedicated MCP server, you empower your AI agents with several critical data layers:

*   **Firmographic Intelligence**: Instant access to verified company size, revenue brackets, and industry classifications.
*   **Technographic Stacks**: Identify exactly what software (SaaS, infrastructure, security) a target company is currently using.
*   **Live Intent Signals**: Retrieve hiring trends and growth triggers that indicate a high propensity to purchase.
*   **Hallucination-Resistant Parameters**: All tools within the server utilize strict **Zod-schema annotations**, ensuring that Cursor or Claude Desktop never provides malformed inputs or hallucinates API parameters.

## IDE Configuration (Cursor & VS Code)

To enable these tools in Cursor or your MCP-enabled IDE, add the following configuration to your `mcpServers` settings file. This points your environment directly to the production-grade lead enrichment endpoint.

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

When the LLM invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This allows the AI to synthesize recommendations based on hard data rather than probabilistic guesses.

```json
{
  "tool": "enrich_lead",
  "parameters": { "domain": "stripe.com" },
  "response": {
    "companyName": "Stripe, Inc.",
    "industry": "Fintech / Payments",
    "technographics": ["AWS", "React", "Kubernetes", "Salesforce"],
    "intentSignals": {
      "hiringVelocity": "High",
      "recentExpansion": true
    },
    "confidenceScore": 0.98,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing

Modern AI workflows demand predictable unit economics. This B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the data is low quality, the match is ambiguous, or the query fails, the cost is $0. This ensures you can scale autonomous SDR swarms and research agents without paying for "I'm sorry, I couldn't find that company" responses.

## Get Started for Free

You can begin integrating live firmographic tools into your AI workflow in under two minutes. Visit the portal to claim your free tier API key and view the full documentation.

**[Get Your B2B Lead Enrichment API Key Now](https://lead-enrichment-mcp.agent-infra.workers.dev)**