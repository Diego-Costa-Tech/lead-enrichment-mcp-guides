# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

Deploying a B2B lead enrichment MCP server provides your local LLM agents with native, real-time access to high-fidelity firmographic and technographic data. By integrating the Model Context Protocol directly into your IDE, you eliminate the need for brittle web scraping or manual CRM lookups, allowing your coding agents to pull verified company profiles directly into the context window.

## Core Features and Data Integrity
Our MCP server is engineered to provide depth through three primary data layers: **firmographics** (revenue, headcount, location), **technographics** (stack analysis), and **intent signals** (market activity indicators). 

Crucially, the server employs **strict Zod schema annotations** for every tool call. This forces the LLM to pass valid, typed parameters, which effectively eliminates the common issue of parameter hallucination where models attempt to pass malformed company names or invalid domain formats to the API.

## Configuring your IDE (Claude Desktop / Cursor)
To connect your agent environment to our live data stream, add the following configuration to your `claude_desktop_config.json` (or the equivalent MCP settings menu in Cursor):

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
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Structure
When you invoke the `enrich_lead` tool, the server returns a standardized JSON-RPC object. Note that the **confidenceScore** field allows your autonomous agents to programmatically decide whether to proceed with a sales outreach or discard the lead based on data quality:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["Kubernetes", "AWS", "Terraform"],
    "intentSignals": "High-intent: recent job postings for DevOps Engineers",
    "confidenceScore": 0.94
  }
}
```

## The Value Proposition: Risk-Free Metered Billing
We prioritize developer velocity and cost efficiency. Our metered billing architecture is designed for production AI workflows: you are billed strictly for successful enrichments where the **Confidence Score exceeds 0.6**. If our system returns a low-confidence result or fails to verify the lead, the operation is **free of charge**. This allows you to build robust, high-volume SDR agent swarms without worrying about wasted spend on noisy or null data points.

## Integrate Real-Time Data Today
Stop relying on static, outdated datasets. Elevate your development workflow by connecting your agent swarm to the most reliable firmographic source in the MCP ecosystem. Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start enriching your leads on the free tier instantly.