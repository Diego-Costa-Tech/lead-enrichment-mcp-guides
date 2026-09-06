# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server. By integrating our B2B lead enrichment MCP server directly into your IDE’s Model Context Protocol configuration, you enable Cursor and VS Code to pull real-time company profiles and technographic signals directly into your agentic workflows.

## Core Features
This MCP server exposes granular data points including **firmographic data** (employee count, revenue ranges), **technographic stacks** (SaaS tools, infrastructure), and **intent signals** (market activity). To eliminate common LLM parameter hallucinations, we utilize strict **Zod schema annotations** for all tool arguments. This ensures that when the LLM triggers an enrichment, the API receives valid parameters like `domain` or `email`, resulting in high-fidelity, actionable data every time.

## Configuring Your IDE
To connect the tool to Cursor or VS Code, add the following configuration to your `mcp.json` or IDE settings file. This points your environment directly to our hosted endpoint:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/mcp-lead-enrichment"],
      "env": {
        "MCP_LEAD_ENRICHMENT_API_KEY": "your_api_key_here",
        "MCP_API_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Payload
The tool returns a standardized object designed for immediate LLM consumption, providing depth beyond simple lookups:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Terraform", "Datadog"],
    "intentSignals": {
      "score": 88,
      "topic": "Migration to Multi-Cloud"
    },
    "confidenceScore": 0.94
  }
}
```

## The Value Proposition: Risk-Free Metering
We prioritize cost-efficiency for developers building autonomous sales agents. Our **risk-free metered billing** model ensures you only pay for high-value data. If our API returns a `confidenceScore` below 0.6, or if the query fails to return structured results, you are not charged. This allows you to scale your autonomous SDR swarms without worrying about "garbage-in, garbage-out" costs, ensuring your AI agents only iterate on verified, high-intent prospects.

## Get Started Today
Ready to arm your AI agents with live market intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start building on our free tier immediately.