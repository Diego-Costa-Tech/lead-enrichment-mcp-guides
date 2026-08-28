# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your IDE’s configuration. By integrating our B2B lead enrichment MCP server, you enable your AI coding agents to fetch real-time company profiles, technographics, and intent signals directly within the chat context, eliminating the need for manual data scraping.

## Core Features and Data Integrity
Our MCP server bridges the gap between static LLM knowledge and dynamic market data. The API provides three primary data layers: **Firmographic Intelligence** (employee count, HQ location, revenue tier), **Technographic Stacks** (installed software, cloud infrastructure), and **Real-time Intent Signals**. To prevent LLM parameter hallucinations, we utilize strict **Zod schema annotations** for every tool definition. This forces the LLM to provide perfectly formatted domain strings and company IDs, ensuring that your agentic workflows execute without runtime serialization errors or invalid API requests.

## Configuring your IDE for MCP
To connect the lead enrichment tool, add the following configuration to your `claude_desktop_config.json` or your Cursor/VS Code MCP configuration file.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/lead-enrichment-mcp"
      ],
      "env": {
        "LEAD_ENRICHMENT_API_KEY": "your_api_key_here",
        "API_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Payload
When the LLM calls the `enrich_lead` tool, it receives a structured, validated JSON response. This allows the model to immediately reason about the target account and adjust its messaging or technical recommendations accordingly.

```json
{
  "jsonrpc": "2.0",
  "id": "req-12345",
  "result": {
    "companyName": "TechScale Solutions",
    "industry": "SaaS / Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Datadog"],
    "intentSignals": {
      "score": 88,
      "topic": "Migrating to microservices"
    },
    "confidenceScore": 0.94
  }
}
```

## The Risk-Free Metered Billing Advantage
Scaling autonomous sales workflows is cost-prohibitive when paying for low-quality data. Our billing model is strictly metered: **you are only billed for successful enrichments where the Confidence Score is > 0.6.** If the tool returns a low-confidence or "no data found" result, the transaction is free. This ensures that your autonomous SDR swarms remain cost-effective and only consume budget when high-fidelity business intelligence is actually delivered.

## Get Your Free API Key
Ready to supercharge your AI agents with enterprise-grade data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start your integration on our generous free tier today.