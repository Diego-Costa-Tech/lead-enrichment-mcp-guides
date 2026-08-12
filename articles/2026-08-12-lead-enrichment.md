# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

To equip Cursor or VS Code with native B2B lead enrichment capabilities, you must integrate a Model Context Protocol (MCP) server that provides real-time company profiles and intent signals directly to the LLM's context window. Using a B2B lead enrichment MCP server allows your AI editor to query firmographics, technographic stacks, and buying intent via standardized JSON-RPC tools, eliminating the need for manual data scraping or context switching.

## Core Features of the Enrichment MCP
This MCP server acts as a bridge between the Model Context Protocol and high-fidelity B2B data providers. By exposing a structured `enrich_lead` tool, it allows LLMs to retrieve deep metadata using only a company domain or email address.

*   **Firmographic Intelligence:** Retrieve real-time data on company revenue, headcount, industry classification, and headquarters location.
*   **Technographic Analysis:** Identify the underlying software stack of a target company, including cloud providers, CRM usage, and marketing automation tools.
*   **Intent Signal Processing:** Access live triggers such as recent funding rounds, hiring surges, or technology shifts.
*   **Zero-Hallucination Schemas:** All tool parameters are defined using strict **Zod annotations**. This forces the LLM to provide valid domains and prevents the "hallucination" of contact data by enforcing a rigid JSON-RPC structure.

## Configuration for Cursor and VS Code
To enable these tools in Cursor or VS Code (via the Claude Dev or Roo Code extensions), add the following configuration to your `mcpServers` settings. This connects your IDE directly to the hosted MCP endpoint.

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "curl",
      "args": [
        "-s",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "API_KEY": "YOUR_PRODUCTION_KEY"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Payload
When the LLM invokes the `enrich_lead` tool, it receives a clean, structured object. This ensures the agent can reason about the data programmatically without parsing messy HTML or unstructured text.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "ExampleCorp",
    "industry": "Enterprise Software",
    "headcount": "500-1000",
    "technographics": ["AWS", "Salesforce", "React"],
    "intentSignals": [
      {"type": "Funding", "detail": "Series B - $40M", "date": "2023-11-15"}
    ],
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing
Traditional B2B data APIs charge per request, regardless of whether the data is accurate or found. This MCP server utilizes a **Confidence-First Billing** model. Your account is only debited for successful enrichments where the `confidenceScore` is greater than 0.6. If the tool returns a "not found" status or low-confidence data, the query cost is $0, making it the most cost-effective solution for building autonomous SDR swarms and high-volume lead processing agents.

## Get Your Free API Key
Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly. Start giving your AI agents the real-world data they need to perform complex B2B sales and research tasks.