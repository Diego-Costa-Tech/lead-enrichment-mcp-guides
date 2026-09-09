# Supercharge Cursor and VS Code with a Live B2B Lead Enrichment MCP Server

Integrating real-time B2B lead enrichment into your IDE via the Model Context Protocol (MCP) allows AI agents like Cursor, VS Code Copilot, or Claude Desktop to fetch live firmographics, technographics, and intent data without manual API calls. By connecting your local environment to a production-grade B2B lead enrichment MCP server, you eliminate data staleness and parameter hallucinations, enabling your AI to reason over actual market data.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to query high-fidelity company data using the Model Context Protocol. Unlike traditional APIs that return messy HTML or unstructured text, this server uses **strict Zod-annotated schemas** to define its tool parameters, ensuring that LLMs like Claude 3.5 Sonnet or GPT-4o generate valid search queries every time.

- **Deep Firmographics:** Access real-time data on employee count, revenue brackets, industry classification, and headquarters location.
- **Technographic Intelligence:** Identify the software stack of a target company (e.g., "Do they use Salesforce or HubSpot?") to tailor outreach logic.
- **Intent & Growth Signals:** Detect hiring trends, recent funding rounds, and expansion signals directly within your coding context.
- **Hallucination Prevention:** By providing a structured tool definition, the LLM is forced to adhere to valid data types, significantly reducing "hallucinated" company details.

## IDE Configuration (Cursor & VS Code)
To give your AI agent access to these tools, add the following configuration to your `project.json` or global MCP settings. This points your environment to the hosted MCP endpoint.

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
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## Structured Data Response Example
When your agent invokes the `enrich_lead` tool, it receives a clean, machine-readable JSON-RPC response. This allows the LLM to process data points as variables rather than raw text, which is critical for building autonomous SDR workflows.

```json
{
  "method": "enrich_lead",
  "result": {
    "companyName": "Acme Corp",
    "domain": "acme.io",
    "industry": "Enterprise SaaS",
    "employeeCount": 1250,
    "technographics": ["AWS", "React", "PostgreSQL", "Segment"],
    "intentSignals": {
      "hiring": "High",
      "recentExpansion": true
    },
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing
Efficiency is at the core of this MCP server. Unlike traditional data providers that charge for every API hit regardless of quality, this system uses a **Risk-Free Metered Billing** structure. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server cannot find a match, or if the data quality falls below the threshold, the cost of the query is $0. This allows developers to build high-volume autonomous swarms without the fear of burning through credits on low-quality leads.

## Get Started with a Free API Key
Ready to upgrade your AI agent with live B2B intelligence? You can grab your free tier API key and view the full documentation in seconds.

Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to register and start enriching leads natively within your Model Context Protocol environment.