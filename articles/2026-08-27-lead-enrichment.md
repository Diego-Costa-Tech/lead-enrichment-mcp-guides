# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

Integrating real-time B2B firmographics into your local development environment is now possible by leveraging an MCP-native B2B lead enrichment server that connects directly to your IDE or LLM client. By deploying the Model Context Protocol (MCP) server, developers can provide Claude Desktop or Cursor with live company profiles, technographics, and intent signals without ever leaving the chat interface.

## Core Features and Data Integrity
The B2B lead enrichment MCP server provides deep insights into account-based marketing (ABM) workflows by surfacing **firmographic data** (revenue, headcount, location), **technographic stacks** (SaaS tools, hosting infrastructure), and **intent signals** (surging interest in specific categories). To solve LLM parameter hallucinations, all tool definitions utilize **strict Zod-schema annotations**, ensuring that the LLM sends valid domain names and company identifiers to the API. This structured approach forces the model to respect the required input constraints before the request is ever sent to the wire.

## Configuring Claude Desktop for Lead Enrichment
To bridge the gap between your local agent and live B2B data, append the following configuration to your `claude_desktop_config.json` file. This setup registers the `enrich_lead` tool natively, allowing Claude to execute lookups in real-time.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/lead-enrichment-mcp"],
      "env": {
        "MCP_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Response Structure
When the LLM calls `enrich_lead(domain: "openai.com")`, the server returns a clean JSON-RPC response designed for high-context ingestion. The confidence score filter ensures the LLM only consumes high-fidelity data:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "OpenAI",
    "industry": "Artificial Intelligence",
    "technographics": ["Kubernetes", "Next.js", "PostgreSQL"],
    "intentSignals": ["Generative AI", "LLM Infrastructure"],
    "confidenceScore": 0.98,
    "employeeCount": "1000+"
  },
  "id": 1
}
```

## Risk-Free Metered Billing
Efficiency is key for autonomous SDR workflows. Our pricing model is strictly pay-per-success. You are only billed for enrichments where the **Confidence Score exceeds 0.6**. If the API fails to find a match or returns low-quality data (Confidence Score < 0.6), the query cost is $0. This ensures that your agent swarm operations remain cost-effective while maintaining high data quality across your prospecting funnel.

## Get Started with MCP Lead Enrichment
Ready to enhance your agent's data awareness? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start streaming real-time firmographic data directly into your Claude or Cursor environment today.