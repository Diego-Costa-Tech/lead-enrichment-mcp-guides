# Building Autonomous SDR Swarms with Firmographic Data via B2B Lead Enrichment MCP

Scaling autonomous SDR agent swarms requires a reliable Model Context Protocol (MCP) server that provides real-time B2B lead enrichment and firmographic intent data directly to LLMs. By integrating the B2B Lead Enrichment MCP API, developers can equip sales agents with the precise company profiles and technographic signals needed to eliminate cold outreach hallucinations and drive conversion.

## Core Features

To build a high-performance sales agent, your LLM needs more than just a name and a domain. This MCP server exposes a high-fidelity data layer designed specifically for the Model Context Protocol, ensuring agents have context-aware capabilities:

*   **Deep Firmographics:** Access validated data on company headcount, annual revenue, industry vertical, and precise geographic headquarters.
*   **Technographic Intelligence:** Identify the underlying tech stack of a target lead (e.g., "Is this lead using AWS or GCP?", "Do they have Salesforce installed?") to tailor outreach.
*   **Intent Signal Mapping:** Retrieve real-time growth signals, including recent funding rounds, hiring surges, and leadership changes.
*   **Zero-Hallucination Schemas:** All tool parameters are defined using strict **Zod annotations**, forcing the LLM to provide valid JSON-RPC requests and preventing common tool-calling errors.

## Claude Desktop & Cursor Integration

To enable your SDR swarm, add the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings. This gives your local AI agent native access to the `enrich_lead` and `get_company_intent` tools.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-b2b-enrichment"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## Clean JSON-RPC Tool Response

When your agent invokes the `enrich_lead` tool, it receives a structured payload optimized for LLM consumption. This ensures the agent can accurately reason about the lead's quality before generating a personalized email or Slack notification.

```json
{
  "status": "success",
  "data": {
    "companyName": "TechScale AI",
    "industry": "Enterprise Software",
    "headcount": "250-500",
    "technographics": ["Kubernetes", "Snowflake", "Stripe"],
    "intentSignals": {
      "recentFunding": "Series B - $45M",
      "hiringVelocity": "High",
      "primarySignal": "Expansion into EMEA"
    },
    "confidenceScore": 0.94,
    "metadata": {
      "lastUpdated": "2023-10-27T14:22:01Z"
    }
  }
}
```

## Risk-Free Metered Billing for SDR Workflows

Building autonomous swarms can be expensive if you pay for every API call, regardless of quality. Our B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** model. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. 

If the data is stale, the company is not found, or the confidence interval is too low for professional outreach, the query cost is $0. This allows you to run massive batch-processing workflows across thousands of leads without worrying about "junk data" inflating your overhead.

## Get Started with the B2B Lead Enrichment MCP

Ready to upgrade your AI sales agents from simple chat bots to data-driven SDR swarms? Visit the portal to generate your API key and access the full technical documentation.

[Get your Free API Key at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)