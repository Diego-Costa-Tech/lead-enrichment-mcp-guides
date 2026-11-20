# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying a Model Context Protocol (MCP) server directly into your IDE. By connecting the B2B Lead Enrichment MCP API to Cursor or VS Code, you enable your AI coding assistant to perform real-time company research, technographic stack identification, and intent signal analysis using standardized JSON-RPC tools.

## Core Features of the B2B Lead Enrichment MCP
Unlike static datasets, this MCP server provides a dynamic bridge to high-fidelity B2B data layers, ensuring your AI agents operate on current reality rather than stale training data. To prevent the common issue of LLM parameter hallucinations, every tool within this server utilizes **strict Zod schema annotations**, forcing the model to provide valid email formats, domain structures, and search parameters.

*   **Real-Time Firmographics:** Instant retrieval of company size, revenue estimates, headquarters location, and industry classification.
*   **Deep Technographics:** Identification of a lead’s current software stack, including CRM usage, cloud providers, and marketing automation tools.
*   **Intent Signal Processing:** Surfacing "ready-to-buy" signals based on recent company news, hiring patterns, and technology shifts.
*   **Confidence Scoring:** Every enrichment includes a `confidenceScore` metadata field, allowing your workflows to programmatically ignore low-probability matches.

## Configuration for Cursor and VS Code
To integrate these tools into Cursor or your local MCP runtime, add the following configuration to your `project.json` or the global MCP settings file. This points your environment to the production-ready hosted endpoint.

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
        "API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Example
When the `enrich_lead` tool is invoked by an LLM like Claude 3.5 Sonnet or GPT-4o, the server returns a clean, structured payload. This allows the AI to synthesize business logic without parsing messy HTML or unformatted text.

```json
{
  "result": {
    "companyName": "Acme Corp",
    "domain": "acme.com",
    "industry": "Enterprise Software",
    "firmographics": {
      "employees": "500-1000",
      "estimatedRevenue": "$50M-$100M",
      "hq": "San Francisco, CA"
    },
    "technographics": ["Salesforce", "AWS", "HubSpot", "Segment"],
    "intentSignals": [
      { "type": "expansion", "description": "Opening new office in EMEA" },
      { "type": "hiring", "role": "Head of Sales" }
    ],
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing Architecture
Building AI-driven sales agents can become expensive if you pay for failed queries or low-quality data. This MCP server implements a developer-first **Risk-Free Metered Billing** structure. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server returns no data, a low-confidence match, or a 404, the cost of that specific API call is $0. This ensures your autonomous SDR swarms remain cost-effective and focus budget only on high-value lead data.

## Get Your Free API Key Today
Ready to upgrade your AI agent's B2B intelligence? Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to generate your API key and access the free tier instantly. Start building firmographically-aware AI tools in minutes.