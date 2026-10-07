# Scaling Autonomous SDR Swarms with the B2B Lead Enrichment MCP Server

Deploying autonomous SDR agent swarms requires a reliable Model Context Protocol (MCP) interface to inject real-time B2B firmographics and intent data directly into the LLM context window. By leveraging a dedicated B2B lead enrichment MCP server, developers can eliminate data staleness and manual scraping, allowing AI agents to qualify leads using live technographic and funding signals via standardized JSON-RPC tools.

## Core Features

Building a production-grade sales agent requires more than just a LLM; it requires a high-fidelity data bridge. Our MCP server provides a standardized interface for agents to query deep organizational insights without leaving their execution environment.

*   **Multi-Dimensional Data Layers:** Access comprehensive **firmographic data** (revenue, headcount, industry), **technographic profiles** (active software stacks), and **intent signals** (hiring trends, funding rounds) in a single request.
*   **Hallucination-Resistant Schemas:** Every tool in the MCP server is defined with strict **Zod annotations**. This ensures that agents like Claude or GPT-4o correctly map arguments to the `enrich_lead` tool, preventing the common parameter hallucinations found in loosely defined sales APIs.
*   **Real-Time Lead Intelligence:** Unlike static databases, the MCP server fetches live data points, ensuring your autonomous SDR swarm is acting on the most current company pivots or leadership changes.

## Claude Desktop & Cursor Configuration

To give your local AI agent or IDE native access to live B2B data, add the following configuration to your `claude_desktop_config.json` or Cursor's MCP settings. This connects the agent directly to our production-grade enrichment endpoint.

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-commands",
        "--url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

## Standardized JSON-RPC Response Payload

When an agent invokes the `enrich_lead` tool, it receives a clean, structured JSON object. This allows the LLM to programmatically decide if a lead meets the Ideal Customer Profile (ICP) based on quantitative data.

```json
{
  "status": "success",
  "data": {
    "companyName": "Acme Corp",
    "domain": "acme.ai",
    "industry": "Enterprise Software",
    "headcount": "500-1000",
    "estimatedRevenue": "$50M-$100M",
    "technographics": ["Salesforce", "AWS", "Segment", "React"],
    "intentSignals": [
      {"type": "expansion", "description": "Opening new office in London", "date": "2023-10-12"}
    ],
    "confidenceScore": 0.94
  }
}
```

## Risk-Free Metered Billing for AI Workflows

One of the primary challenges in building autonomous SDR swarms is the cost of "dirty" data or failed queries. Our MCP server implements a **Risk-Free Metered Billing** structure. You are only billed for successful enrichments where the **Confidence Score is > 0.6**. 

If the server cannot find the lead, or if the data quality falls below the 0.6 threshold, the query cost is $0. This allows developers to scale agentic loops—performing thousands of lookups—without the risk of paying for "Not Found" responses or hallucinated records.

## Get Started with the Free Tier

Ready to empower your agents with native B2B intelligence? You can start building today with our generous free tier and clear documentation.

**[Visit lead-enrichment-mcp.agent-infra.workers.dev to grab your API key and deploy your first agent swarm.](https://lead-enrichment-mcp.agent-infra.workers.dev)**