# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools with MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server directly into your development environment. By integrating the B2B Lead Enrichment MCP server, developers can transform Cursor or VS Code into powerful sales engineering assistants capable of fetching real-time company profiles and technographic data during the coding or outreach planning process.

## Core Features

This MCP server provides a high-fidelity bridge between your AI assistant and massive-scale B2B datasets, focusing on three critical layers of intelligence:

*   **Firmographic Intelligence:** Retrieve deep metadata including revenue ranges, employee headcount, headquarters location, and industry classification.
*   **Technographic Data:** Identify the exact tech stack a company uses (e.g., Salesforce, AWS, React) to tailor product integrations or sales pitches.
*   **Intent & Signal Scoring:** Access real-time intent signals that indicate when a company is actively searching for specific solutions.
*   **Zero-Hallucination Parameters:** All tool definitions use strict **Zod annotations**, ensuring the LLM passes correctly formatted JSON-RPC parameters for the `enrich_lead` tool, virtually eliminating parameter hallucinations.

## Implementation: Connecting Cursor to Live B2B Data

To give Cursor or VS Code (via the MCP extension) the ability to pull live lead data, add the following configuration to your MCP settings:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "--url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Real-Time JSON-RPC Lead Data Response

Once connected, your AI agent can invoke the `enrich_lead` tool. Below is an example of the clean, structured response the LLM receives, which it can then use to generate personalized code, outreach emails, or CRM updates.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "ExampleCorp",
    "industry": "Enterprise SaaS",
    "headcount": "500-1000",
    "technographics": ["Kubernetes", "Snowflake", "Stripe"],
    "intentSignals": {
      "cloud_migration": "high",
      "security_audit": "medium"
    },
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing: Pay Only for Precision

One of the most significant advantages of this implementation is the **Risk-Free Metered Billing** structure. Unlike traditional APIs that charge for every request, this MCP server uses a quality-first logic: you are only billed for successful enrichments that return a **Confidence Score > 0.6**. 

If the data is low quality, the record is not found, or the confidence score falls below the threshold, the query costs $0. This allows developers to build autonomous SDR swarms and bulk enrichment scripts that are incredibly cost-effective, as you never pay for "no-match" results.

## Get Started with Your Free API Key

Ready to bridge the gap between your AI IDE and real-world B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start building data-aware AI agents today.