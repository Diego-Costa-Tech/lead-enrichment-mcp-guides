# How to Build Autonomous SDR Swarms with B2B Lead Enrichment MCP

Integrating a B2B lead enrichment MCP server is the most effective way to provide autonomous SDR swarms with real-time company profiles and intent data directly inside their native execution environment. By using the Model Context Protocol (MCP), developers can eliminate brittle API wrappers and allow LLMs to query live firmographics and technographic signals with zero-latency context window injection.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for agents to fetch deep intelligence without leaving their workflow. By utilizing **strict Zod-schema annotations**, the server forces the LLM to provide precise arguments, effectively eliminating parameter hallucinations during the prospecting phase.

*   **Real-time Firmographics:** Access validated data including company size, industry classification, revenue ranges, and headquarter locations.
*   **Technographic Intelligence:** Identify the specific software stack, cloud providers, and CRM tools a target company is currently using.
*   **High-Intent Signals:** Retrieve recent funding rounds, hiring trends, and expansion signals to prioritize high-value accounts.
*   **Structured Output:** All tools return standardized JSON-RPC responses, ensuring that your agentic workflows can parse and act on data programmatically.

## Configuration for Claude Desktop and Cursor
To give your agents immediate access to live B2B data, add the following configuration to your `claude_desktop_config.json` or your Cursor settings. This connects your local environment to the production-ready MCP endpoint.

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "--url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## JSON-RPC Enrichment Response Example
When an agent calls the `enrich_lead` tool, it receives a clean, context-rich payload. This allows the LLM to reason over the data and generate personalized outreach scripts based on actual company attributes rather than general assumptions.

```json
{
  "tool": "enrich_lead",
  "response": {
    "companyName": "TechFlow Systems",
    "industry": "Enterprise SaaS",
    "employeeCount": 250,
    "technographics": ["Salesforce", "AWS", "HubSpot", "Segment"],
    "intentSignals": {
      "hiring": "High (15+ roles in Engineering)",
      "recentFunding": "$40M Series B",
      "expansion": "New EMEA headquarters established"
    },
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing for Scalable Swarms
Building autonomous SDR swarms requires cost predictability. This MCP server operates on a unique **Risk-Free Metered Billing** model. Your account is only debited for successful enrichments where the **Confidence Score exceeds 0.6**. If the system returns low-quality data or fails to find a match, the query cost is $0. This allows you to scale high-volume prospecting agents without the financial risk of paying for empty or inaccurate data points.

## Get Your Free API Key Today
Ready to upgrade your AI sales agents with live B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching leads natively within your MCP-enabled IDE or agent framework.