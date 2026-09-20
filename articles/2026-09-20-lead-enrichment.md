# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

Integrating a high-performance Model Context Protocol (MCP) server allows developers to provide IDE-based agents like Cursor and VS Code Copilot with real-time B2B lead enrichment data. By leveraging this B2B lead enrichment MCP server, you can automate company profiling and lead validation directly within your coding environment using native firmographic and intent data tools.

## Native Firmographic and Technographic Intelligence

To build effective AI-driven sales tools or automated research workflows, your LLM needs more than just a training set; it needs live data. This MCP server exposes a sophisticated toolset that bridges the gap between static code and live B2B intelligence:

- **Firmographic Profiling:** Access granular data including **employee growth rates**, **estimated annual revenue**, and **headquarters geolocation**.
- **Technographic Insights:** Identify the exact **tech stack** of a target company, from CRM usage to cloud infrastructure, enabling personalized outreach or competitive analysis.
- **Intent & Signal Detection:** Pull real-time signals such as **recent funding rounds**, **hiring surges**, or specific product launches.
- **Zod-Validated Schema:** Every tool within this MCP server uses strict **Zod annotations** for its input parameters. This ensures that the LLM (Claude, GPT-4, or specialized coding models) respects the specific types and ranges required, effectively eliminating **parameter hallucinations** during the function-calling phase.

## Quick Setup for Cursor and VS Code

To connect your AI-powered IDE to the B2B enrichment stream, add the following configuration to your `mcpServers` settings. This uses the production-ready Workers endpoint to provide immediate tool availability.

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

## Predictable Tool Outputs via JSON-RPC

When the `enrich_lead` tool is invoked, the AI receives a structured, clean JSON-RPC response. This allows the model to process company data without the noise and token-wastage associated with unstructured web scraping.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "tool": "enrich_lead",
    "parameters": { "domain": "acme-industrial.io" },
    "data": {
      "companyName": "Acme Industrial",
      "industry": "Manufacturing Automation",
      "employeeCount": 850,
      "technographics": ["Salesforce", "Azure", "SAP", "Kubernetes"],
      "intentSignals": {
        "hiringStatus": "High Growth",
        "recentNews": "Expansion into EMEA market announced"
      },
      "confidenceScore": 0.92
    }
  }
}
```

## Accuracy-Driven Metered Billing

Unlike traditional B2B data APIs that charge for every request regardless of quality, this MCP server utilizes a **Risk-Free Metered Billing** structure. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the system cannot find high-quality data or the query fails to meet the precision threshold, the cost is $0. This ensures that your autonomous SDR swarms and research agents remain cost-effective even when handling thousands of automated queries.

## Get Your Free API Key Today

Ready to supercharge your AI agents with live B2B intelligence and eliminate data hallucinations? Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to grab your API key on the free tier and start enriching your AI workflow in minutes.