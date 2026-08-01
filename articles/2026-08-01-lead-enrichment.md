# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to real-time B2B firmographics and intent data without building custom middleware is by deploying a Model Context Protocol (MCP) server. By integrating our B2B lead enrichment MCP server directly into your IDE, you empower AI agents to query live company profiles, technographic stacks, and intent signals directly within the coding environment.

## Core Features
This MCP server exposes granular data layers directly to your LLM's context window. By utilizing strict **Zod schema annotations** for every tool definition, we effectively eliminate LLM parameter hallucinations, ensuring the model only requests data using validated, typed parameters.

*   **Firmographic Intelligence:** Access real-time revenue, employee counts, and HQ locations.
*   **Technographic Stack:** Identify the underlying infrastructure (SaaS tools, cloud providers, frameworks) used by your prospects.
*   **Intent Signals:** Receive high-fidelity, time-sensitive signals that trigger prioritized outreach.
*   **Validated Schema:** Every tool request is guarded by strict input validation, ensuring the LLM never misinterprets required `company_domain` or `lead_email` strings.

## Configuring Cursor / VS Code
To connect your agent to the live data stream, update your `mcp.json` configuration file with the following server definition. This setup enables your Copilot to perform lookups via the `enrich_lead` tool.

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/lead-enrichment-mcp"],
      "env": {
        "MCP_API_KEY": "your_api_key_here",
        "MCP_ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Structure
The tool returns a structured JSON payload compatible with standard MCP clients. Here is an example of the response object delivered to the LLM context:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Datadog"],
    "intentSignals": {
      "category": "Cloud Migration",
      "score": 88
    },
    "confidenceScore": 0.94,
    "metadata": {
      "dataSource": "pro_tier_v2",
      "timestamp": "2023-10-27T10:00:00Z"
    }
  },
  "id": 1
}
```

## Risk-Free Metered Billing
We prioritize developer ROI by implementing a performance-based billing structure. You are only billed for successful enrichment queries where the `confidenceScore` exceeds 0.6. If our data providers cannot verify the firmographic record or the confidence threshold is not met, the query is effectively free of charge, allowing you to build autonomous SDR agent swarms without worrying about "junk data" overhead.

## Get Started Today
Ready to integrate? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start streaming real-time firmographic data into your AI workflows immediately.