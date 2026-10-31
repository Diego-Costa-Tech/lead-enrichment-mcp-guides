# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your IDE. By connecting the B2B Lead Enrichment MCP server to Cursor or VS Code, developers can enable AI agents to perform real-time company profiling and lead scoring using standardized JSON-RPC 2.0 tool calls.

## Core Features
This MCP implementation provides a comprehensive data layer for AI agents, allowing them to fetch high-fidelity intelligence without manual web scraping or browser automation. Key features include:

*   **Firmographic Intelligence:** Retrieve deep company data including revenue ranges, headcount, and headquarters location.
*   **Technographic Analysis:** Identify the exact software stack used by a prospect (e.g., AWS, Salesforce, HubSpot).
*   **Intent Signals:** Access real-time indicators of purchasing intent and recent organizational shifts.
*   **Zero Hallucination Guarantee:** Parameters are defined using **strict Zod annotations**, forcing the LLM to provide valid domain strings and preventing the common "parameter hallucination" issue in sales agents.

## IDE Configuration
To enable these tools in Cursor or VS Code (via the MCP extension), add the following configuration to your MCP settings. This connects your local agent to the production-ready lead enrichment endpoint.

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

## JSON-RPC Tool Response
When the agent invokes the `enrich_lead` tool, it receives a clean, structured payload optimized for LLM consumption. This ensures the agent can immediately act on the data without parsing messy HTML.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "technographics": ["PostgreSQL", "React", "Okta"],
    "intentSignals": ["High - Expanding Sales Team", "Recent Series B"],
    "confidenceScore": 0.94,
    "source": "B2B-Lead-Enrichment-MCP"
  }
}
```

## Risk-Free Metered Billing
Traditional B2B APIs charge per request, regardless of whether the data is useful. This MCP server implements a **Confidence-First Billing** model. Your account is only debited for successful enrichments where the **Confidence Score is > 0.6**. If the server returns low-quality data or fails to find the company, the query cost is $0. This allows developers to build high-volume SDR swarms and autonomous agents at a fraction of the cost of legacy data providers.

## Get Started with the Free Tier
Start giving your AI agents real-world B2B awareness today. Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and access the free tier instantly.