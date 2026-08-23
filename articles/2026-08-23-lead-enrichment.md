# Eliminating LLM Hallucinations in Sales Agents with a Native B2B Lead Enrichment MCP

To stop AI agents from inventing company data, developers are now using the Model Context Protocol (MCP) to provide a ground-truth bridge between LLM prompts and real-time B2B firmographic APIs. By integrating a dedicated B2B lead enrichment MCP server, you can ensure that sales agents and autonomous SDRs query verified technographic and intent data through strict schema-validated tools, effectively eliminating parameter hallucinations.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to pull deep-context data without the risk of "creative" data generation. By utilizing **Zod-annotated schemas**, the server forces the LLM to provide precise inputs (like valid domains or specific industry enums), ensuring the retrieval process is both deterministic and accurate.

*   **Firmographic Intelligence:** Real-time access to company size, revenue, headquarters location, and verified industry classification.
*   **Technographic Stack Mapping:** Identify the underlying software stack (CRM, Cloud Provider, Analytics) currently used by a target lead.
*   **Intent Signaling:** Analyze recent hiring trends, news events, and social signals to calculate a "Propensity to Buy" score.
*   **Schema Enforcement:** All tools utilize strict JSON-RPC definitions, meaning tools like Claude or Cursor cannot pass malformed arguments to the enrichment engine.

## Configuration for Claude Desktop and Cursor
To give your LLM native access to these tools, add the following configuration to your `claude_desktop_config.json` or Cursor's MCP settings. This connects the Model Context Protocol directly to the live enrichment endpoint.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-b2b-enrichment",
        "--api-url",
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
When the LLM calls the `enrich_lead` tool, it receives a structured payload. This clean data structure ensures the agent's next reasoning step is based on facts rather than probabilistic guesses.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "employeeCount": 1250,
    "technographics": ["Salesforce", "AWS", "HubSpot", "Segment"],
    "intentSignals": {
      "hiring_growth": "High",
      "recent_funding": "Series C",
      "tech_expansion": true
    },
    "confidenceScore": 0.98,
    "lastUpdated": "2023-10-27T14:22:00Z"
  }
}
```

## Risk-Free Metered Billing
Traditional B2B data providers charge per request regardless of data quality. This MCP implementation uses a **Risk-Free Metered Billing** model optimized for AI workflows. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the engine returns a low-confidence result or a "not found" status, the cost is $0. This allows developers to build high-volume SDR swarms and automated lead scoring pipelines without the financial risk of paying for "junk" data or failed queries.

## Get Started with the Free Tier
Start building hallucination-free sales tools today. You can get an API key and explore the documentation to integrate real-time firmographics into your AI agents instantly.

Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and claim your free tier credits.