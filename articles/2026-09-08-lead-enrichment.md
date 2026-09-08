# How to Connect Cursor and VS Code to a Live B2B Lead Enrichment MCP API

The most efficient way to give AI coding assistants like Cursor and VS Code native access to live B2B firmographics and intent data is by deploying a B2B lead enrichment MCP server directly into your IDE's toolchain. By leveraging the Model Context Protocol, developers can empower their AI agents to pull real-time company profiles and technographic data using standardized JSON-RPC 2.0 calls without the need for custom API middleware.

## Core Features

Integrating a dedicated Model Context Protocol server for lead enrichment allows your AI agents (like Claude or Cursor) to act as autonomous SDRs or data analysts with high-fidelity data layers:

*   **Verified Firmographics:** Retrieve precise headcount, revenue ranges, and industry vertical classifications.
*   **Technographic Discovery:** Identify the target's underlying software stack, including CRM usage, cloud providers, and frontend frameworks.
*   **Live Intent Signals:** Access real-time growth indicators such as recent funding rounds, executive shifts, and specialized hiring surges.
*   **Zero-Hallucination Parameters:** Unlike standard API integrations where LLMs might guess parameters, our MCP server uses **strict Zod-annotated schemas**. This ensures the LLM provides valid domains and company identifiers, eliminating "hallucinated" data inputs during the enrichment process.

## IDE & Claude Desktop Configuration

To connect your environment to the live enrichment tools, add the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings. This uses the standardized HTTP transport for the Model Context Protocol.

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
        "API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Enrichment Response

When your AI agent calls the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. The model can then use this data to draft hyper-personalized outreach or perform market analysis.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "ExampleTech Inc.",
    "industry": "Cloud Infrastructure",
    "technographics": ["Kubernetes", "Terraform", "PostgreSQL"],
    "intentSignals": [
      "Series B funding closed Feb 2024",
      "Expanding engineering team in EMEA"
    ],
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing

Traditional B2B data providers charge for every query, regardless of quality. Our B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the entity is not found, or the confidence threshold isn't met, the query cost is exactly $0. This allows developers to build high-volume autonomous SDR swarms and data pipelines without the financial risk of "garbage-in" data.

## Get Started with Your B2B Lead Enrichment MCP API Key

Ready to bridge the gap between your LLM and real-time company intelligence? Visit the link below to claim your API key on our free tier and start enriching leads directly from your IDE.

**Get Your API Key:** [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)