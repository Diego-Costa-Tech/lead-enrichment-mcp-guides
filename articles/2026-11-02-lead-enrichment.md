# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Integrating a real-time B2B lead enrichment MCP server directly into your IDE allows Cursor and VS Code agents to perform deep firmographic research and intent analysis without leaving the code editor. By utilizing the Model Context Protocol, developers can eliminate LLM parameter hallucinations and provide AI agents with a Zod-validated stream of live company data and technographic signals.

## Core Features
This MCP-native server provides a programmatic bridge between B2B data lakes and your LLM-powered development environment. By exposing specific tools via the JSON-RPC standard, it enables:

*   **Real-time Firmographics:** Instant retrieval of company size, industry classification, revenue ranges, and headquarters location.
*   **Technographic Intelligence:** Identification of a target's current tech stack, including CRM, cloud providers, and analytics tools.
*   **Intent Data & Signals:** Native access to hiring trends, funding history, and expansion signals to prioritize outreach.
*   **Strict Zod Schema Validation:** All input parameters for the `enrich_lead` tool are strictly typed, ensuring the LLM passes valid domains and company names, which drastically reduces tool-calling errors.

## IDE Configuration (Cursor / VS Code / Claude Desktop)
To give your agent access to live B2B data, add the following configuration to your MCP settings file (e.g., `project.json` for Cursor or `claude_desktop_config.json`).

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
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

## JSON-RPC Response Example
When the LLM invokes the `enrich_lead` tool, it receives a structured payload optimized for context injection. The following example demonstrates the high-fidelity data returned by the server:

```json
{
  "tool": "enrich_lead",
  "status": "success",
  "data": {
    "companyName": "Acme Corp",
    "domain": "acme.io",
    "industry": "Enterprise SaaS",
    "headcount": "500-1000",
    "technographics": ["Salesforce", "AWS", "Segment", "React"],
    "intentSignals": {
      "recentFunding": "Series C",
      "hiringVelocity": "High",
      "expansionSignals": ["New EMEA Office"]
    },
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing
Efficiency is baked into the protocol. This MCP server utilizes a risk-free metered billing structure designed for autonomous SDR agents and AI workflows. You are only billed for successful enrichments that return a **Confidence Score greater than 0.6**. If the data is low quality, or if the entity cannot be found, the query cost is $0. This allows for massive-scale scraping and lead filtering within Cursor or VS Code without the risk of paying for "No Results Found" responses.

## Get Started with a Free API Key
Ready to upgrade your AI agents with real-world B2B intelligence? Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to grab your API key on the free tier and start enriching leads directly within your IDE today.