# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to real-time B2B firmographics and intent data without custom middleware is by deploying an MCP-native B2B lead enrichment MCP server. By integrating this protocol directly into your IDE, you enable autonomous agents to fetch verified company profiles and technographic data without suffering from the context-window limitations or hallucination risks of static training data.

## Core Features
Our **B2B lead enrichment MCP server** provides deep-stack data access directly to your AI agents via the **Model Context Protocol (MCP)**. Key features include:

*   **Firmographic Data:** Access granular details including employee count, HQ location, and revenue brackets.
*   **Technographic Intelligence:** Identify tech stacks, SaaS integrations, and infrastructure patterns to qualify prospects.
*   **Intent Signals:** Real-time scoring of buying intent to prioritize high-value leads.
*   **Strict Zod Schema Enforcement:** All API calls are wrapped in rigorous **Zod annotations**, forcing the LLM to provide correct arguments, effectively eliminating parameter hallucinations during tool invocation.

## IDE Configuration
To enable the MCP server in your local environment, append the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings.

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
        "MCP_API_KEY": "YOUR_API_KEY_HERE",
        "API_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Payload
The tool returns structured, clean data designed for immediate agent processing. Below is a sample response from the `enrich_lead` tool:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": {
      "score": 88,
      "category": "High Intent - Demo Request"
    },
    "confidenceScore": 0.95
  }
}
```

## Risk-Free Metered Billing
Efficiency is at the core of this integration. Our pricing model is strictly metered, meaning you are only billed for successful enrichments where the **Confidence Score > 0.6**. If the API fails to find a match or returns low-confidence data, the query costs $0, ensuring your autonomous SDR swarms remain cost-effective while scaling.

## Get Your API Key
Ready to supercharge your development workflow with live B2B intelligence? Head over to [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start utilizing the free tier for your agentic applications today.