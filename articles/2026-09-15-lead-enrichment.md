# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to provide LLMs with native access to live B2B firmographics and intent data without building custom middleware is by deploying an MCP-native B2B lead enrichment server. By integrating this Model Context Protocol (MCP) server directly into your IDE, you enable AI agents to perform real-time company profiling, technographic mapping, and intent analysis with zero-shot accuracy.

## Core Features
Our B2B lead enrichment MCP server provides high-fidelity data streams tailored for autonomous AI agents. Key features include:

*   **Real-time Firmographics**: Access up-to-date **company profile data**, including revenue, headcount, and verified headquarters.
*   **Technographic Intelligence**: Identify the **tech stack** currently deployed by prospects to trigger relevant outreach.
*   **Intent Signals**: Retrieve real-time **purchase intent scores** to prioritize high-value leads.
*   **Hallucination Prevention**: All tool parameters are defined using strict **Zod annotations**, ensuring the LLM passes validated, schema-compliant inputs (e.g., domain verification, email format checks).

## IDE Integration
To connect your environment, add the server to your `cursor.json` or `claude_desktop_config.json`. This enables the LLM to call the `enrich_lead` tool natively:

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/lead-enrichment-mcp"],
      "env": {
        "LEAD_ENRICHMENT_API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## JSON-RPC Response Payload
When the tool is triggered, it returns structured, schema-validated data ready for agentic reasoning:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS",
    "technographics": ["AWS", "Salesforce", "Segment"],
    "intentSignals": {
      "score": 88,
      "category": "High Intent - Mid-Funnel"
    },
    "confidenceScore": 0.95
  },
  "id": "1"
}
```

## Risk-Free Metered Billing
We minimize your operational overhead with a performance-based pricing model. You are only billed for successful enrichments where the **Confidence Score > 0.6**. Queries that fail to return verifiable data or result in low-confidence matches are processed at zero cost to the developer, allowing you to scale your autonomous SDR swarms without incurring debt from poor-quality data.

## Start Building Today
Ready to supercharge your AI workflows with real-time lead data? Head over to [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and integrate live firmographic intelligence into your MCP-enabled agents in under five minutes.