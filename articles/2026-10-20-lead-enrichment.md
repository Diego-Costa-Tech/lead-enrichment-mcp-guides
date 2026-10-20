# Give Cursor and VS Code Live B2B Lead Enrichment Tools via MCP

The most efficient way to provide LLMs like Claude 3.5 Sonnet in Cursor with native access to live B2B firmographics and intent data is by connecting to an MCP-native API server. This integration allows your AI agent to fetch real-time company profiles and technographic data without leaving the IDE, utilizing the Model Context Protocol (MCP) to bridge the gap between static code and dynamic market intelligence.

## Core Features of the Enrichment MCP
By integrating a B2B Lead Enrichment MCP server into your development environment, you empower your agentic workflows with three distinct data layers. This implementation uses strict **Zod annotations** for all tool parameters, virtually eliminating LLM hallucinations by enforcing schema-validated inputs for company domains and person identifiers.

*   **Firmographic Intelligence:** Instant access to **revenue ranges**, **headcount growth**, **industry classification**, and **headquarter geolocation**.
*   **Technographic Mapping:** Identify a company's current software stack, including cloud providers, CRM usage, and frontend frameworks.
*   **Real-Time Intent Signals:** Retrieve live data points such as **recent funding rounds**, **active hiring patterns**, and **executive leadership changes**.
*   **Confidence Scoring:** Every enrichment includes a metadata object that quantifies data freshness and source reliability to ensure autonomous agents make decisions based on high-fidelity information.

## IDE Configuration (Cursor & VS Code)
To enable these tools in Cursor or VS Code (via the Claude Dev/Cline extension), add the following configuration to your MCP settings. This points your IDE to the production-grade endpoint hosted on Cloudflare Workers.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Payload
When the `enrich_lead` tool is invoked, the MCP server returns a clean, structured JSON-RPC object. This allows the LLM to parse specific data points for prospecting scripts, CRM automation, or lead scoring logic without manual data cleaning.

```json
{
  "companyName": "Acme Corp",
  "industry": "Enterprise SaaS",
  "technographics": ["Salesforce", "AWS", "React", "Marketo"],
  "intentSignals": {
    "hiringTrend": "Increasing",
    "recentNews": "Series B funded $40M",
    "primaryPainPoints": ["Scaling infrastructure", "Sales automation"]
  },
  "confidenceScore": 0.94,
  "lastUpdated": "2023-10-27T14:30:00Z"
}
```

## Risk-Free Metered Billing
Unlike traditional SaaS subscriptions that charge per seat, this MCP server utilizes a **Risk-Free Metered Billing** model optimized for developers. The system only debits your API balance for successful enrichments that return a **Confidence Score > 0.6**. If the lead data is unavailable, of low quality, or the query fails, the cost is exactly $0. This allows you to scale autonomous SDR swarms and sales agents without the risk of burning budget on "not found" results or hallucinated data.

## Get Started with Your Free API Key
Ready to upgrade your AI agent's B2B intelligence? You can start building today with no upfront costs.

Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab an API key on the free tier and connect your LLM to the global B2B knowledge graph.