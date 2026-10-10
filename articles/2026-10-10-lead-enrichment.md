# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to provide your LLMs with native access to live B2B firmographics and intent data without custom middleware is by deploying a B2B lead enrichment MCP server directly into your IDE. By utilizing the Model Context Protocol, developers can now ground autonomous agents in real-time company profiles, effectively eliminating stale context and data-drift in sales automation workflows.

## Core Features
Our MCP server bridges the gap between static training data and live market intelligence. By implementing strict Zod schemas for all tool definitions, we force the LLM to adhere to structured inputs, preventing the parameter hallucinations common in loosely typed API calls. The API provides three primary data layers:
*   **Firmographics:** Standardized company metadata, including employee count, revenue bands, and headquarters location.
*   **Technographics:** Deep insights into the current software stack, identifying competitor usage and infrastructure choices.
*   **Intent Signals:** Real-time triggers based on job postings, funding rounds, and web traffic surges.

## IDE Configuration for Cursor / Claude Desktop
To integrate the B2B Lead Enrichment MCP API, append the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings. Use the production endpoint: `https://lead-enrichment-mcp.agent-infra.workers.dev/mcp`.

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

## JSON-RPC Response Payload Example
When an agent invokes `enrich_lead`, the MCP server returns a validated, schema-compliant JSON-RPC response. Note the inclusion of the `confidenceScore` to ensure your agent pipelines only process high-fidelity data.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "TechCorp Solutions",
    "industry": "SaaS Infrastructure",
    "technographics": ["AWS", "Docker", "Kubernetes", "Stripe"],
    "intentSignals": {
      "fundingRound": "Series B",
      "hiringTrend": "Growth"
    },
    "confidenceScore": 0.92
  }
}
```

## The Value Proposition: Risk-Free Metered Billing
Efficiency is at the core of our infrastructure. Our unique billing model is built for scale; you are only charged for successful enrichments where the **Confidence Score > 0.6**. If our system returns low-quality data or fails to find a match, your query costs $0, allowing you to build autonomous SDR agent swarms without the risk of burning your budget on null results.

## Get Started with the Free Tier
Ready to upgrade your agent's knowledge base? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start integrating live, verified B2B intelligence into your development environment instantly.