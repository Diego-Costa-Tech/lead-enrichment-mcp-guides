# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to provide LLMs with native access to live B2B firmographics and intent data without building custom middleware is by deploying an MCP-native B2B lead enrichment server. By integrating our MCP-native API directly into your development environment, you eliminate the latency and context-switching typically associated with manual lead research by pulling verified company profiles directly into your coding IDE.

## Core Features
This Model Context Protocol server exposes high-fidelity data layers designed for autonomous agents and developer workflows:
*   **Firmographic Data:** Precise company size, revenue, and verified headquarters locations.
*   **Technographic Stack:** In-depth insights into the software infrastructure and SaaS tools currently used by the target organization.
*   **Intent Signals:** Real-time triggers based on active market movement and hiring patterns.
*   **LLM Hallucination Mitigation:** All MCP tool parameters are defined using strict **Zod annotations**, ensuring the LLM understands input constraints and enforces valid JSON schemas before firing requests, drastically reducing structural errors.

## MCP Configuration for Cursor/VS Code
To connect the enrichment tool, add the following entry to your `mcp.json` configuration file located in your IDE's application support directory:

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
        "API_KEY": "your_api_key_here",
        "API_URL": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Structure
The `enrich_lead` tool returns a standardized object, allowing your agent to parse firmographics without complex text processing:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["Kubernetes", "AWS", "Terraform"],
    "intentSignals": ["Active hiring for DevOps", "Funding Series C"],
    "confidenceScore": 0.92
  },
  "id": 1
}
```

## The Value Proposition: Risk-Free Metered Billing
We operate on a "Quality-First" pricing model. You are only billed for successful enrichments where the **Confidence Score > 0.6**. If the API returns a low-quality or failed query, you pay $0. This allows developers to build robust autonomous SDR swarms and research agents without worrying about "dead" API costs eating into your project budget.

## Get Started Instantly
Integrate live, verified B2B intelligence into your AI stack today. Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and access the free tier instantly.