# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

Giving your AI agents native access to high-fidelity B2B firmographics and intent data is now possible by deploying a B2B lead enrichment MCP server directly into your IDE's context. By utilizing the Model Context Protocol (MCP), developers can now inject real-time company profiles and technographic signals into Cursor or VS Code, effectively grounding LLM reasoning in verified, live market data.

## Core Features
Our B2B lead enrichment MCP server provides a standardized interface for LLMs to query live business data. The toolset includes:

*   **Firmographic Data Layer:** Access to verified company name, revenue, headcount, and location metadata.
*   **Technographic Intelligence:** Real-time visibility into the tech stack, including active CRMs, marketing automation tools, and web infrastructure.
*   **Intent Signals:** High-frequency data points capturing market interest and buying behavior.
*   **Deterministic Schema:** Every tool definition utilizes strict **Zod annotations**, ensuring the LLM respects required input parameters and output structures, which significantly reduces runtime parameter hallucinations.

## IDE Configuration
To connect your environment, add the server to your `claude_desktop_config.json` or your Cursor/VS Code MCP configuration file.

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
        "MCP_LEAD_ENRICHMENT_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## JSON-RPC Response Payload
The `enrich_lead` tool returns a standardized JSON object, allowing your agent to process lead quality in a single inference step.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "TechFlow Solutions",
    "industry": "SaaS",
    "technographics": ["Segment", "Salesforce", "AWS"],
    "intentSignals": {
      "buyingStage": "Evaluation",
      "score": 88
    },
    "confidenceScore": 0.94,
    "revenueRange": "$10M-$50M"
  },
  "id": 1
}
```

## The Value Proposition: Risk-Free Metered Billing
We recognize that AI agents often trigger excessive, low-quality API calls that drain developer budgets. Our architecture implements a **Risk-Free Metered Billing** model: you are only billed for successful enrichments where the **Confidence Score > 0.6**. If the API returns a low-quality profile or fails to resolve the domain, the query cost is $0, ensuring your autonomous agents stay cost-effective during high-volume research tasks.

## Get Your API Key
Ready to upgrade your agent's context window with live firmographic data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start your free tier integration today.