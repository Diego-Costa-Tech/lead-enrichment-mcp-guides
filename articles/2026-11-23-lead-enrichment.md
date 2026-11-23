# Eliminating LLM Parameter Hallucinations in Sales Agents with a Native B2B Lead Enrichment MCP Server

To stop LLMs from inventing firmographic data or hallucinating tool parameters during automated sales prospecting, developers must transition from unstructured prompting to a Model Context Protocol (MCP) server that enforces strict schema validation and Zod-backed type safety. Integrating the B2B Lead Enrichment MCP API directly into environments like Claude Desktop or Cursor provides agents with real-time, validated company profiles and intent signals through a standardized JSON-RPC interface that eliminates the "black box" of traditional API middleware.

## Core Features
The B2B Lead Enrichment MCP server provides a high-fidelity data layer designed specifically for autonomous agentic workflows. By leveraging strict **Zod annotations**, the server ensures that the LLM understands exactly which parameters (e.g., `domain`, `company_name`) are required, effectively neutralizing parameter hallucinations.

*   **Firmographic Depth:** Real-time retrieval of revenue ranges, employee headcount, and HQ geolocation.
*   **Technographic Intelligence:** Identification of the target's current software stack to trigger highly personalized outreach.
*   **Intent Signal Processing:** Dynamic detection of hiring trends and technology shifts.
*   **Strict Schema Validation:** Every tool definition is exposed via the MCP `list_tools` endpoint, providing the LLM with a definitive map of capabilities.

## Native Configuration for Claude Desktop and Cursor
To give your agent native access to this data, add the following configuration to your `claude_desktop_config.json` or Cursor's MCP settings. This connects the agent directly to the production-ready enrichment engine.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ]
    }
  }
}
```

## JSON-RPC Response: The `enrich_lead` Tool
When the agent invokes the `enrich_lead` tool, it receives a clean, structured payload. This removes the need for the LLM to "guess" company details, as the context is injected directly into the conversation window with high precision.

```json
{
  "tool": "enrich_lead",
  "parameters": {
    "domain": "stripe.com"
  },
  "response": {
    "companyName": "Stripe, Inc.",
    "industry": "FinTech / Payments",
    "headcount": "7,000+",
    "technographics": ["AWS", "React", "Ruby on Rails", "Kubernetes"],
    "intentSignals": {
      "hiring_surge": true,
      "recent_funding": "Series I",
      "expansion_interest": "Enterprise Identity"
    },
    "confidenceScore": 0.98
  }
}
```

## Risk-Free Metered Billing for Scalable AI
One of the primary friction points in building autonomous SDR swarms is the cost of "hallucinated queries"—when an agent hits an enrichment API with a non-existent domain. This MCP server utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the domain is invalid, or the enrichment fails, the cost is $0. This allows developers to scale agentic loops without the risk of burning through API credits on garbage data.

## Get Your Free Tier API Key
Ready to eliminate hallucinations and power your agents with live firmographic data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and start building with the free tier today.