# How to Connect Cursor and VS Code to a Live B2B Lead Enrichment MCP API

To give LLMs native access to real-time B2B firmographics and intent data without building custom middleware, developers are now deploying the B2B lead enrichment MCP server directly into their IDEs and AI agents. By utilizing the Model Context Protocol (MCP), your AI agent can instantly query live company profiles and technographic data using standardized JSON-RPC tools, effectively turning your editor into a high-performance sales intelligence engine.

## Core Features of the B2B Lead Enrichment MCP
The Model Context Protocol (MCP) solves the "knowledge cutoff" problem by allowing agents like Cursor, Claude Desktop, and VS Code Copilot to call external APIs as if they were local functions. This specific MCP server provides three critical data layers:

*   **Deep Firmographics:** Access real-time data on company size, revenue, headquarters, and industry classification.
*   **Technographic Stack:** Identify the specific software, cloud infrastructure, and tools a company is currently using.
*   **Intent & Signal Detection:** Extract actionable insights based on recent hiring trends, funding rounds, and growth metrics.
*   **Hallucination Prevention:** All parameters are governed by strict **Zod schemas**, ensuring the LLM passes valid arguments (like valid domain strings or email formats) to the `enrich_lead` tool, eliminating typical API-calling errors.

## Implementation: Cursor and Claude Desktop Configuration
To integrate these tools, add the following configuration to your MCP settings file. This points your agent to the hosted Worker environment where the B2B lead enrichment logic resides.

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

## JSON-RPC Response Architecture
When your AI agent invokes the `enrich_lead` tool, it receives a structured JSON payload designed for immediate token injection. This allows the model to reason about the lead with high precision.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "technographics": ["AWS", "Salesforce", "React", "Snowflake"],
    "intentSignals": {
      "hiring": "High (15+ roles in DevOps)",
      "funding": "Series C (March 2024)"
    },
    "confidenceScore": 0.94,
    "source": "verified_firmographic_index"
  }
}
```

## Risk-Free Metered Billing for AI Agents
One of the primary challenges in building autonomous SDR swarms is the cost of low-quality data. This MCP server implements a **Confidence-First Billing** model. You are only billed for successful enrichments where the **Confidence Score is > 0.6**. If the server returns a "No result found" or the data quality is too low to be actionable, the query cost is exactly $0. This allows developers to scale agentic workflows and lead-gen bots without worrying about burning through credits on unverified data.

## Get Your Free B2B Enrichment API Key
Ready to upgrade your AI agent with live B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly. Start building autonomous sales workflows that actually have the data they need to convert.