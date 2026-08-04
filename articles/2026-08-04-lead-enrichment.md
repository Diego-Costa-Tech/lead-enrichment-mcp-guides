# How to Equip Cursor and VS Code Copilot with Live B2B Lead Enrichment via MCP

The most direct method for providing LLMs in Cursor and VS Code Copilot native access to live B2B firmographics and intent data is through a Model Context Protocol (MCP) bridge. By utilizing a dedicated B2B lead enrichment MCP server, developers enable AI agents to retrieve real-time company profiles and technographic details with zero-latency middleware.

## Core Features

This MCP server transforms your AI coding assistant into a powerful sales engineering tool by providing access to deep data layers:

*   **Deep Firmographics**: Real-time retrieval of company size, revenue brackets, and industry NAICS/SIC classifications.
*   **Technographic Mapping**: Identify the specific software stack, cloud providers, and development tools used by any domain.
*   **Intent Signals**: Surface high-propensity buying signals and recent organizational changes directly within the LLM context window.
*   **Hallucination Prevention**: Every tool within the server utilizes strict **Zod annotations** to enforce parameter types, ensuring that AI agents provide valid queries and receive structured, verifiable data.

## Configuring Cursor and VS Code Copilot

To integrate these tools into your IDE, add the following configuration to your MCP settings. This connects your environment to the production-grade endpoint.

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
      ]
    }
  }
}
```

## Example Lead Enrichment Response

When you trigger the `enrich_lead` tool within your IDE, the AI receives a clean, structured JSON-RPC response. This allows the LLM to reason about the company without guessing metadata.

```json
{
  "status": "success",
  "data": {
    "companyName": "Acme Corp",
    "industry": "Enterprise Software",
    "headcount": "500-1000",
    "technographics": ["AWS", "Kubernetes", "React", "Salesforce"],
    "intentSignals": {
      "hiring_growth": "high",
      "tech_stack_expansion": "active"
    },
    "confidenceScore": 0.94
  }
}
```

## Success-Only Metered Billing

Unlike traditional B2B data providers that charge per query regardless of quality, this MCP server utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the data is low quality, or if the lead cannot be found, the cost is exactly $0. This allows developers to build high-volume autonomous SDR swarms and sales tools without the risk of burning credits on "empty" responses.

## Get Your Free API Key

Ready to bridge the gap between your IDE and live B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab an API key on the free tier and start enriching leads natively in your workflow today.