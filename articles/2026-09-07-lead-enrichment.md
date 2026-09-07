# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native B2B lead enrichment MCP server directly into your IDE. By integrating this Model Context Protocol interface, you allow your coding assistants to query real-time company profiles and technographic data without leaving your development environment.

## Core Features
This MCP server exposes a standardized set of tools designed for deep data synthesis:
*   **Firmographic Data:** Retrieve real-time **company size**, **revenue buckets**, and **headquarters location**.
*   **Technographic Intelligence:** Access granular data on **tech stacks**, **infrastructure providers**, and **SaaS utilization**.
*   **Intent Signals:** Filter leads by high-intent triggers, mapped through **Zod-validated parameters** to ensure 100% type safety.
*   **Hallucination Prevention:** By enforcing strict schema definition for every parameter, the MCP server forces the LLM to provide exact inputs (e.g., valid domains, ISO-country codes), effectively eliminating parameter hallucinations common in unstructured RAG workflows.

## Configuration for Cursor/VS Code
To connect the enrichment tool, add the following configuration to your `mcp.json` file (typically located in `~/Library/Application Support/Cursor/User/globalStorage/mcp-server.json` or equivalent VS Code config directory):

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": ["-y", "@agent-infra/mcp-enrichment-client"],
      "env": {
        "MCP_API_KEY": "your_api_key_here",
        "MCP_API_URL": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Structure
When the LLM triggers the `enrich_lead` tool, the server returns a structured JSON-RPC payload optimized for context injection:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Datadog"],
    "intentSignals": ["High", "Recent Series B"],
    "confidenceScore": 0.92
  },
  "id": 1
}
```

## The Value Proposition: Risk-Free Metered Billing
We prioritize developer ROI by implementing a **Confidence-Based Billing model**. You are only billed for enrichments where the **Confidence Score > 0.6**. If the API cannot reliably verify a company profile or returns low-quality data (Confidence Score ≤ 0.6), the query is marked as a failure and costs **$0**. This allows you to build autonomous SDR agent swarms without worrying about "garbage-in, garbage-out" expenses draining your credits.

## Get Started Instantly
Stop guessing firmographics. Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key and integrate professional-grade B2B intelligence into your AI workflow today.