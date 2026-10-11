# How to Give Cursor and Claude Desktop Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to real-time company profiles and firmographics without custom middleware is by deploying a B2B lead enrichment MCP server directly into your development environment. By leveraging the Model Context Protocol (MCP), developers can grant Claude Desktop and Cursor autonomous, secure access to live B2B intent data, effectively turning your AI assistant into a high-octane research agent.

## Core Features and Data Integrity
Our **B2B lead enrichment MCP server** provides deep-level access to three primary data layers: **firmographics** (revenue, headcount, location), **technographics** (tech stack, software installation markers), and **intent signals** (buying signals, market movement). To solve the common issue of LLM parameter hallucinations, we utilize strict **Zod-based schema validation** for every tool call. This ensures that the model only receives sanitized, strongly-typed company domains, preventing execution errors and ensuring your agents only query what they are explicitly designed to handle.

## Configuring Cursor or Claude Desktop
Add the following configuration to your `claude_desktop_config.json` (for Claude) or the `.cursor/mcp.json` file (for Cursor) to bridge the gap between your local agent and our live production endpoint.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@mcp/lead-enrichment-sdk",
        "--api-url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "LEAD_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## JSON-RPC Response Payload
The tool returns a validated, structured JSON-RPC object. This structured data allows the LLM to process business logic immediately, such as qualifying a lead for an SDR workflow based on the `confidenceScore`.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS / Fintech",
    "technographics": ["Stripe", "AWS", "Salesforce"],
    "intentSignals": ["series_b_funding", "hiring_sdr"],
    "confidenceScore": 0.92,
    "revenueRange": "$10M-$50M"
  },
  "id": "1"
}
```

## Risk-Free Metered Billing
We prioritize developer ROI with a risk-free metered billing model. You are only billed for successful enrichments where the **Confidence Score exceeds 0.6**. If our system returns a low-quality profile or fails to resolve the firmographic data, your usage cost for that request is exactly $0. This allows you to build autonomous agent swarms at scale without the fear of burning budget on incomplete or hallucinated data.

## Start Building Your Research Agents
Ready to automate your outbound research or internal data enrichment? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start your free tier integration today.