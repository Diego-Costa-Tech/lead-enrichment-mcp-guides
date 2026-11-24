# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Integrating a real-time B2B lead enrichment MCP server into Cursor or VS Code allows AI coding assistants to access live firmographic and intent data without leaving the editor. This architectural approach leverages the Model Context Protocol to provide LLMs with a structured, ground-truth data layer for building sales-tech integrations, automating CRM workflows, or generating targeted outbound codebases.

## Core Features
The B2B Lead Enrichment MCP API provides a robust bridge between LLMs and live market data, specifically designed to solve the data-stale nature of standard training sets.

*   **Deep Firmographics:** Access real-time employee counts, revenue brackets, and headquarters locations via the `enrich_lead` tool.
*   **Technographic Intelligence:** Query the specific software stacks and infrastructure choices (e.g., AWS, React, Salesforce) of target companies.
*   **Intent Signal Mapping:** Retrieve high-intent signals to prioritize leads based on active technology shifts or funding rounds.
*   **Zero-Hallucination Parameters:** Every tool input is strictly enforced via **Zod schema annotations**, ensuring Cursor or VS Code Copilot provides valid JSON-RPC requests every time.

## Cursor & VS Code Configuration
To enable these tools, add the following configuration to your `project.json` or your global MCP settings file (typically found in `~/Library/Application Support/Cursor/mcp_config.json`).

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "curl",
      "args": [
        "-s",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
When your AI agent calls the `enrich_lead` tool, it receives a structured JSON-RPC payload. This clean data structure allows the LLM to process information without the noise of HTML scraping or unstructured PDF parsing.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["Kubernetes", "Terraform", "Stripe"],
    "intentSignals": "Expansion into EMEA market",
    "confidenceScore": 0.94,
    "employeeCount": 1250,
    "lastUpdated": "2023-10-27T14:22:00Z"
  }
}
```

## Risk-Free Metered Billing
Unlike traditional SaaS subscriptions that charge high monthly retainers, this MCP server utilizes a performance-based metered billing model. Users are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the server returns low-quality data or fails to find the entity, the request is cost-free ($0), making it the most cost-effective solution for building autonomous SDR swarms and high-volume lead processing pipelines.

## Get Your Free API Key Instantly
Ready to upgrade your AI agent's knowledge? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start enriching leads natively within your IDE today.