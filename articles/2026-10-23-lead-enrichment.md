# Eliminating LLM Hallucinations in Sales Agents with a Native B2B Lead Enrichment MCP Server

To stop LLMs from hallucinating company firmographics and contact details, developers must shift from prompt-based knowledge to a schema-strict Model Context Protocol (MCP) server for real-time B2B lead enrichment. Deploying a native B2B lead enrichment MCP server allows agents to fetch validated company profiles and intent signals using Zod-enforced parameters that eliminate tool-call errors in Claude, Cursor, and VS Code.

## Core Features

Integrating high-fidelity data into your AI workflows requires more than just an API; it requires a protocol-aware bridge. Our MCP server implements strict **Zod-validated schemas** to ensure that LLMs like Claude 3.5 Sonnet or GPT-4o never pass malformed arguments.

*   **Deep Firmographics:** Access real-time data including employee count, revenue brackets, industry classification, and headquarters location.
*   **Technographic Intelligence:** Identify the specific software stack (e.g., Salesforce, AWS, HubSpot) used by a target company to tailor outreach.
*   **Intent Signals:** Track high-value triggers such as recent funding rounds, executive transitions, or hiring surges.
*   **Zero Hallucination Guarantee:** By using the Model Context Protocol, the LLM is provided with a structural definition of the `enrich_lead` tool, preventing it from "guessing" metadata that isn't present in the source database.

## Claude Desktop & Cursor Configuration

To give your AI agent native access to this B2B intelligence, add the following configuration to your `claude_desktop_config.json` or your Cursor "MCP Servers" settings. This connects your environment directly to our production-ready enrichment engine.

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

## JSON-RPC Response Example

When your agent invokes the `enrich_lead` tool, it receives a clean, structured payload. This allows the LLM to parse the data with 100% accuracy rather than extracting text from a messy HTML scrape.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Example Corp",
    "industry": "Enterprise Software",
    "technographics": ["Kubernetes", "Snowflake", "Okta"],
    "intentSignals": {
      "funding": "Series C - $50M",
      "hiring": "Expansion in EMEA"
    },
    "confidenceScore": 0.98,
    "metadata": {
      "source": "Verified Business Registry",
      "lastUpdated": "2023-10-27T10:00:00Z"
    }
  }
}
```

## Risk-Free Metered Billing

We solve the "bad data cost" problem by implementing a performance-based billing model. Traditional APIs charge you for every request, regardless of whether they find a match. Our MCP server uses a **Confidence-First Billing** system:

1.  **High-Confidence Matches:** You are only billed for enrichments that return a **Confidence Score > 0.6**.
2.  **Failed/Low-Quality Queries:** If our engine cannot find the lead or the data is outdated (Confidence Score < 0.6), the request costs exactly **$0**.
3.  **Autonomous-Ready:** This allows you to build SDR swarms that can process thousands of leads without worrying about runaway costs from unverified or low-quality data entries.

## Get Started with a Free API Key

Ready to turn your LLM into a data-driven sales powerhouse? Visit our documentation and dashboard to claim your free tier API key and start enriching leads with the Model Context Protocol today.

[Visit lead-enrichment-mcp.agent-infra.workers.dev to get your API key](https://lead-enrichment-mcp.agent-infra.workers.dev)