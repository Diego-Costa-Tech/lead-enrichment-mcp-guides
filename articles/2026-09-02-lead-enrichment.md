# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

To equip AI coding assistants like Cursor and VS Code with native B2B lead enrichment capabilities, you must integrate a Model Context Protocol (MCP) server that provides real-time firmographic and intent data directly to the LLM's context window. By leveraging the B2B lead enrichment MCP server, developers can bypass manual data scraping and ensure their sales automation scripts or SDR agents have immediate access to high-confidence company profiles and technographic signals without leaving their IDE.

## Core Features
The B2B Lead Enrichment MCP API provides a robust bridge between AI agents and live data silos. It utilizes **strict Zod-schema annotations** to define tool parameters, effectively eliminating LLM hallucinations when the model attempts to map company names to data points.

*   **Firmographic Intelligence:** Retrieve real-time data on company size, revenue brackets, and HQ locations.
*   **Technographic Data:** Identify the software stack (e.g., Salesforce, AWS, HubSpot) a target company is currently using.
*   **Intent Signals:** Surface high-intent triggers such as recent funding rounds, hiring surges, or technology migrations.
*   **Confidence Scoring:** Every enrichment includes a precision metric to ensure autonomous agents only act on high-veracity data.

## Implementation: Connecting to Cursor or Claude Desktop
To give your LLM access to these tools, add the following configuration to your `claude_desktop_config.json` or your Cursor MCP settings. This configuration uses the MCP-native Workers endpoint to serve tools directly to your local agent.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Clean JSON-RPC Tool Response
When your agent invokes the `enrich_lead` tool, it receives a structured payload. This clean data injection allows the LLM to reason about a prospect with perfect accuracy, rather than guessing details based on training data cutoff dates.

```json
{
  "tool_use": "enrich_lead",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Enterprise SaaS",
    "technographics": ["Kubernetes", "Snowflake", "Okta"],
    "intentSignals": {
      "hiring": "High",
      "funding": "Series C (March 2024)"
    },
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing for SDR Swarms
Building autonomous SDR swarms requires a cost-effective data strategy. This MCP server utilizes a **Risk-Free Metered Billing** structure specifically designed for AI agents. Unlike legacy APIs that charge for every request, you are only billed for successful enrichments that return a **Confidence Score > 0.6**. 

If the tool returns a low-quality match or fails to find the company, the query cost is $0. This allows developers to scale "shotgun" enrichment workflows across thousands of leads without worrying about the high costs of data decay or failed lookups.

## Get Started with Your Free API Key
Ready to turn your AI coding assistant into a powerful sales intelligence engine? Visit the portal to claim your free tier API key and start enriching leads natively within your MCP-enabled environment.

**Visit: [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)**