# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools

Integrating a Model Context Protocol (MCP) server for real-time B2B lead enrichment allows LLMs to pull live firmographic and technographic profiles directly into the IDE context window. By deploying our B2B lead enrichment MCP server, you eliminate the need for manual API middleware and provide your AI agents with verified, high-fidelity business intelligence instantly.

## Core Features
The MCP API provides a standardized interface for LLMs to query deep data sets including **firmographic data** (revenue, headcount, location), **technographic stacks** (CRM usage, hosting providers, advertising partners), and **intent signals** (buying cycles, market interest). To solve the common issue of LLM parameter hallucinations, our schema utilizes strict **Zod-validated annotations** for all tool arguments. This ensures that the LLM sends valid domains and correctly formatted search queries before the network request is ever dispatched to our engine.

## Configuring your IDE for MCP Enrichment
To enable this in Cursor or VS Code, add the following configuration to your `mcp.json` file or your IDE's global MCP settings. This configuration binds the `enrich_lead` tool directly to your editor's AI capabilities:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/lead-enrichment-mcp",
        "--api-key",
        "YOUR_API_KEY_HERE"
      ],
      "env": {
        "MCP_URL": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Example
When the LLM triggers an enrichment, the API returns a structured JSON-RPC object, providing the AI agent with a high-confidence payload for decision-making:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": "High - Recent Series C funding",
    "confidenceScore": 0.94
  },
  "id": 1
}
```

## Risk-Free Metered Billing
We prioritize developer ROI by implementing a confidence-gated billing model. You are only billed for successful enrichments where the **Confidence Score > 0.6**. Queries that fail to resolve or return ambiguous, low-quality data result in zero charges, allowing you to scale your AI workflows without worrying about unpredictable API costs.

## Get Started Today
Ready to arm your AI agents with live market intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start using our free tier to supercharge your SDR workflows and AI-driven sales research.