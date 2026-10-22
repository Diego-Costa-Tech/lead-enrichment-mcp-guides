# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Integrating live B2B lead enrichment into your development environment is most effectively achieved by connecting your IDE to a dedicated Model Context Protocol (MCP) server. This approach allows Cursor and VS Code Copilot to access real-time firmographic, technographic, and intent data natively through the `enrich_lead` tool, eliminating manual data entry and preventing LLM parameter hallucinations.

## Core Features of the B2B Enrichment MCP
The B2B Lead Enrichment MCP API provides a high-fidelity data bridge between raw company domains and actionable intelligence. By utilizing strict **Zod-annotated schemas**, the server ensures that LLMs provide precise inputs, significantly reducing the "hallucination rate" typically found when agents guess company attributes.

*   **Deep Firmographics:** Access real-time data on employee count, revenue brackets, industry classification (SIC/NAICS), and headquarters location.
*   **Technographic Stack Tracing:** Identify the software tools and infrastructure a company uses (e.g., AWS vs. GCP, CRM choices, or frontend frameworks).
*   **Live Intent Signals:** Retrieve recent growth indicators or funding events that signal a high propensity to purchase.
*   **Strict Parameter Validation:** Every tool call is validated against a schema, ensuring the LLM passes a valid `domain` or `company_name` before execution.

## IDE Configuration for Cursor and VS Code
To enable these capabilities in Cursor or VS Code (via the MCP extension), add the following configuration to your settings. This connects your environment to the production-grade Worker endpoint.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-fetch",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Tool Response Example
When the LLM triggers the `enrich_lead` tool, it receives a structured JSON response. This allows the AI agent to reason about the lead quality based on objective data rather than training-set weights.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise Software",
    "technographics": ["Salesforce", "AWS", "React", "Next.js"],
    "intentSignals": {
      "hiringTrend": "Aggressive",
      "recentFunding": "Series C",
      "expansionScore": 0.88
    },
    "confidenceScore": 0.94,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing Architecture
Unlike traditional SaaS APIs that charge for every request, this MCP server utilizes a **Risk-Free Metered Billing** structure designed for autonomous agents. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data is low quality, incomplete, or the search fails, the cost is exactly $0. This allows developers to build large-scale SDR swarms and automated research pipelines without the risk of burning credits on "Not Found" responses or LLM retry loops.

## Get Started with a Free API Key
Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to claim your free tier API key and start enriching your AI agents with real-time B2B intelligence today.