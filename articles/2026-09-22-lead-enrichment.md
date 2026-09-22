# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to provide LLMs with native access to live B2B firmographics and intent data without custom middleware is by deploying a B2B lead enrichment MCP server. By integrating this Model Context Protocol interface directly into your IDE, you enable Cursor and VS Code to resolve real-time company profiles and technographics as verified tool calls rather than relying on stale, hallucinated training data.

## Core Features and Data Integrity
This MCP server exposes a standardized set of tool definitions that allow LLMs to query high-fidelity business intelligence endpoints. To eliminate the risk of LLM parameter hallucinations, all tools utilize strict **Zod-based input validation**, ensuring that queries for `domain` or `companyName` are structured correctly before the request ever hits the origin.

The data layers include:
*   **Firmographic Data:** Headcount, revenue range, and verified office locations.
*   **Technographic Stack:** In-depth detection of software procurement and infrastructure.
*   **Intent Signals:** Real-time triggers based on recent funding, job postings, and market activity.
*   **Confidence Scoring:** Every output includes a `confidenceScore` parameter, ensuring the agent only acts on data points exceeding a 0.6 threshold.

## Configuration for Cursor and VS Code
To connect your IDE to the production endpoint, update your `mcp.json` configuration file located in your MCP settings directory. This enables the agent to natively invoke the `enrich_lead` function during your coding or research sessions.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/lead-enrichment-mcp"],
      "env": {
        "MCP_API_KEY": "your_api_key_here",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## Example JSON-RPC Response Payload
When the LLM calls `enrich_lead`, the API returns a structured object designed for immediate tokenization and reasoning:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS / Fintech",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": "Series C funding, high hiring velocity in engineering",
    "confidenceScore": 0.94,
    "status": "success"
  },
  "id": "req-12345"
}
```

## Cost-Effective, Risk-Free Metered Billing
We understand that autonomous agents can be chatty. To protect your budget, this API utilizes a **Risk-Free Metered Billing structure**. You are only charged for successful enrichments where the returned `confidenceScore` is > 0.6. Queries that return low-quality data or fail to retrieve a company profile cost exactly $0, allowing you to scale your AI-driven SDR workflows without unpredictable infrastructure costs.

## Get Your API Key
Ready to supercharge your development workflow with live B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start utilizing enterprise-grade firmographic data within your IDE today.