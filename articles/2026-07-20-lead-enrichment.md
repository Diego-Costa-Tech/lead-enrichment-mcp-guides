# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native B2B lead enrichment server. By integrating this B2B lead enrichment MCP server directly into your IDE's environment, you enable your agents to retrieve real-time company profiles and technographic datasets with zero-latency configuration.

## Core Features
Our MCP server bridges the gap between your agent's reasoning capabilities and live **firmographic data**, **technographic stacks**, and **buying intent signals**. To solve the common issue of LLM parameter hallucination, we utilize strict **Zod-based input validation** for every tool call. 

Key data points returned via the protocol include:
*   **Firmographics:** Standardized company size, revenue, and headquarters data.
*   **Technographics:** A granular breakdown of the company's SaaS stack.
*   **Intent Signals:** Real-time scores identifying active procurement behaviors.
*   **Confidence Scoring:** A 0.0 to 1.0 rating ensuring you only trigger workflows on high-quality data.

## IDE Integration Configuration
To connect your environment, add the following to your `claude_desktop_config.json` or Cursor's MCP settings. This configuration authenticates your agent directly against the production MCP endpoint.

```json
{
  "mcpServers": {
    "lead-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/lead-enrichment-mcp"
      ],
      "env": {
        "MCP_API_KEY": "your_api_key_here",
        "API_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Payload
The tool returns a clean, structured JSON-RPC object, ensuring that downstream agent logic can consume the data without parsing overhead.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise Software",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": {
      "score": 0.88,
      "topic": "Cloud Infrastructure"
    },
    "confidenceScore": 0.95
  },
  "id": "1"
}
```

## The Value Proposition: Risk-Free Metered Billing
Efficiency in AI agent development requires strict cost control. Our architecture features a **Risk-Free Metered Billing** model. You are only billed for successful enrichments where the **Confidence Score > 0.6**. If the system returns low-quality data or fails to identify the entity, the request cost is exactly $0. This ensures your autonomous SDR swarms operate with financial predictability while maintaining high data hygiene.

## Get Started Today
Ready to arm your AI agents with enterprise-grade B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and activate the free tier immediately.