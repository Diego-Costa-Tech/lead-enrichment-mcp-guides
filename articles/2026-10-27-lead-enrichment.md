# Eliminating LLM Hallucinations in Sales Agents with a Native B2B Lead Enrichment MCP Server

To stop LLMs from hallucinating company data or fabricating contact details, developers must use the Model Context Protocol (MCP) to enforce strict schema validation for B2B lead enrichment. By deploying an MCP-native server, you provide LLMs like Claude or GPT-4 with a ground-truth toolset that uses Zod-validated input schemas and structured JSON outputs for real-time firmographic and intent data.

## Core Features

Building a reliable sales agent requires moving beyond basic RAG and into structured tool-calling. The **B2B Lead Enrichment MCP API** solves the "hallucination gap" by implementing the Model Context Protocol directly at the edge, ensuring that any AI agent (whether in Claude Desktop, Cursor, or a custom SDR swarm) follows a rigid data contract.

*   **Strict Parameter Validation:** Every tool input, such as `domain` or `company_name`, is wrapped in **Zod-annotated schemas**. This prevents the LLM from passing malformed strings or "guessing" parameters that don't exist in the API specification.
*   **Multi-Layered Firmographics:** Retrieve deep-tier data including **Employee Count, Annual Revenue, NAICS Codes, and HQ Location** with sub-second latency.
*   **Live Intent & Technographics:** Identify the prospect's current tech stack (e.g., "Using Salesforce and AWS") and real-time **Intent Signals** like recent funding rounds or aggressive hiring trends.
*   **Deterministic JSON-RPC Layer:** By utilizing the MCP standard, the communication between the LLM and the enrichment engine is handled via JSON-RPC, removing the ambiguity of natural language extraction and replacing it with machine-readable precision.

## Configuration for Claude Desktop & Cursor

To integrate these tools into your local development environment or your AI agent's runtime, add the following configuration to your `claude_desktop_config.json` or your project's `.cursorrules`.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Structured Tool Response Example

When your agent invokes the `enrich_lead` tool, it receives a clean, deterministic payload. This structure allows the LLM to reason about the lead quality without needing to parse messy HTML or unstructured text.

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "CloudScale Systems",
          "industry": "Cloud Infrastructure",
          "technographics": ["Terraform", "Datadog", "Azure"],
          "intentSignals": ["High", "Recent expansion into EMEA"],
          "confidenceScore": 0.98,
          "isQualified": true
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing

Traditional B2B data providers charge for every API call, even if the data is stale or the confidence is low. Our MCP server implements a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments where the **Confidence Score > 0.6**. 

If the data is unavailable, the match is weak, or the query fails, the cost is exactly **$0**. This allows you to scale autonomous SDR swarms that can "bulk-scan" thousands of domains without the risk of burning your budget on low-quality hits.

## Get Started with the Free Tier

Stop letting your AI agents guess who your prospects are. Deploy a production-grade, MCP-compliant enrichment layer in under 60 seconds.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to claim your API key and start enriching leads for free.**