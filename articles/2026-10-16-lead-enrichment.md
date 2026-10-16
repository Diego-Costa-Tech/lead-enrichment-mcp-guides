# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to provide LLMs with live B2B firmographics and intent data without managing custom middleware is by deploying an MCP-native B2B lead enrichment server. By integrating this Model Context Protocol (MCP) server, developers can enable Cursor or VS Code Copilot to query real-time company profiles and technographics directly within their development workflow, eliminating data staleness.

## Core Features
Our B2B lead enrichment MCP server provides a standardized interface for LLMs to retrieve structured intelligence. Key capabilities include:
*   **Firmographic Data:** Access high-fidelity records including company size, revenue brackets, and HQ locations.
*   **Technographic Stack:** Identify underlying infrastructure, SaaS integrations, and cloud hosting providers.
*   **Intent Signals:** Real-time scoring based on web activity and market behavior to prioritize outreach.
*   **Zod-Validated Parameters:** Every tool definition utilizes strict Zod schema annotations, ensuring the LLM passes correctly formatted domain identifiers and avoiding common parameter hallucinations during recursive search loops.

## Integrating with Cursor/Claude Desktop
To enable the tool, add the following configuration to your `claude_desktop_config.json` or Cursor MCP settings. This registers the endpoint as a native capability for the AI agent:

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/lead-enrichment-mcp",
        "--api-key",
        "YOUR_API_KEY_HERE"
      ],
      "env": {
        "API_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Payload
When the LLM triggers the `enrich_lead` tool, it receives a strongly-typed JSON-RPC response designed for high-context ingestion:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS",
    "technographics": ["AWS", "Stripe", "Next.js"],
    "intentSignals": {
      "score": 88,
      "category": "High Interest"
    },
    "confidenceScore": 0.94
  },
  "id": "uuid-1234-5678"
}
```

## Risk-Free Metered Billing
We prioritize developer ROI with a "pay-for-performance" model. Our billing structure ensures you are only charged for successful enrichments where the **Confidence Score > 0.6**. Any query resulting in a low-quality match or data failure costs exactly $0, allowing you to build autonomous SDR agent swarms without worrying about wasted token or API spend on junk data.

## Get Started Today
Ready to arm your AI agents with enterprise-grade lead intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly.