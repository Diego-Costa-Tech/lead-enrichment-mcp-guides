# Supercharge Cursor and VS Code with Real-Time B2B Lead Enrichment via MCP

To eliminate the manual research gap in AI-driven development and outreach, developers can now integrate the Model Context Protocol (MCP) to provide Cursor and VS Code Copilot with native access to live B2B firmographic and intent data. By connecting to a dedicated B2B lead enrichment MCP server, your IDE-based agents can verify company data, analyze technographic stacks, and generate high-context code or communications directly within their execution context.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to query deep organizational data without leaving the workspace. By leveraging **Model Context Protocol**, the server exposes tools that return high-fidelity data objects structured for agentic consumption.

*   **Real-time Firmographics:** Access up-to-date company size, revenue estimates, and HQ location data.
*   **Technographic Profiling:** Identify the specific software stack (SaaS, Cloud providers, CRM) used by a target domain.
*   **Intent Signals:** Detect organizational changes or growth patterns that signal a high propensity to purchase.
*   **Hallucination Prevention:** Every tool parameter is defined using strict **Zod annotations**, ensuring the LLM passes valid domains and identifiers while respecting the protocol's type safety.

## Configuration for Cursor and VS Code
To give your IDE-based agents (like Cursor's Composer or VS Code Copilot) access to these tools, add the following configuration to your `mcpServers` settings file.

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
        "API_KEY": "YOUR_ENRICHMENT_API_KEY"
      }
    }
  }
}
```

## Reliable JSON-RPC Data Payloads
When the LLM invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This allows the model to reason over the data rather than guessing at company details.

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Dynamics",
    "industry": "Cloud Infrastructure",
    "technographics": ["AWS", "Kubernetes", "Salesforce", "PostgreSQL"],
    "intentSignals": {
      "hiringTrend": "aggressive",
      "techStackExpansion": "AI/ML infrastructure"
    },
    "confidenceScore": 0.94,
    "lastUpdated": "2023-10-27T14:22:10Z"
  }
}
```

## Risk-Free Metered Billing
Traditional data APIs charge for every request, regardless of whether the data is useful. This MCP server implements a **Risk-Free Metered Billing** structure designed for autonomous agents. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the system cannot find a reliable match or the data quality is low, the query cost is exactly $0, making it the most cost-effective solution for high-volume SDR swarms and discovery bots.

## Get Your Free API Key
Ready to upgrade your AI agents with real-time B2B intelligence? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab an API key on our free tier and start enriching leads directly in your terminal or IDE.