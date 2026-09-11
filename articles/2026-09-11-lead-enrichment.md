# Connecting Claude Desktop to a Live B2B Lead Enrichment MCP API for Real-Time Firmographics

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your local environment. This integration allows your AI agent to execute a B2B lead enrichment MCP server toolset to fetch real-time company profiles, technographics, and verified contact data using the Model Context Protocol.

## Core Features of the Enrichment MCP Server

To bridge the gap between static LLM training data and the volatile nature of corporate intelligence, this MCP implementation provides a standardized interface for real-time data retrieval. Unlike generic search tools, this server utilizes **strict Zod-annotated schemas** for every tool parameter, effectively eliminating LLM parameter hallucinations during complex lead research tasks.

*   **Deep Firmographics:** Access headcount trends, revenue estimates, and accurate industry classifications (NAICS/SIC).
*   **Technographic Intelligence:** Identify the target company's current software stack, including CRM, cloud providers, and marketing automation tools.
*   **Intent Signal Processing:** Retrieve real-time signals indicating a company is in an active buying cycle for specific categories.
*   **Hallucination-Resistant Parameters:** Every tool call (e.g., `enrich_lead`) requires specific data types that guide the LLM to provide valid domain names and company identifiers.

## Implementation: Claude Desktop Configuration

To enable these tools in Claude Desktop, add the following configuration to your `claude_desktop_config.json` file. This tells Claude how to communicate with the remote MCP endpoint via an SSE (Server-Sent Events) bridge or a local fetcher.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-fetch",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Tool Response

When your agent invokes the `enrich_lead` tool, the MCP server returns a clean, structured JSON-RPC object. This ensures the LLM receives high-density data that it can immediately use for drafting personalized outreach or conducting competitive analysis.

```json
{
  "tool": "enrich_lead",
  "response": {
    "companyName": "Acme Corp",
    "domain": "acme.io",
    "industry": "Enterprise SaaS",
    "technographics": ["Salesforce", "AWS", "HubSpot", "Segment"],
    "intentSignals": [
      {"type": "hiring_expansion", "score": 0.85},
      {"type": "tech_stack_change", "score": 0.92}
    ],
    "confidenceScore": 0.98,
    "status": "verified"
  }
}
```

## Risk-Free Metered Billing for AI Workflows

Building cost-effective autonomous SDR swarms requires predictable unit economics. This B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the server returns "low quality" data, a failed match, or a confidence score below the threshold, the query cost is exactly $0. This allows developers to scale agentic workflows without the risk of paying for hallucinated or empty data sets.

## Get Your Free API Key Today

Ready to give your AI agents real-world B2B intelligence? Visit the documentation to secure your API key and start building.

[Get Started at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)