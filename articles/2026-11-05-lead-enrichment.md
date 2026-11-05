# How to Give Cursor and VS Code Copilot Live B2B Lead Enrichment Tools via MCP

Integrating real-time firmographics into your IDE is now possible by connecting a B2B lead enrichment MCP server directly to Cursor or VS Code via the Model Context Protocol. This setup allows your AI coding assistant to fetch live company profiles, technographic stacks, and intent signals natively, eliminating parameter hallucinations through strict Zod-validated schemas.

## Core Features
The B2B Lead Enrichment MCP API provides a standardized interface for LLMs to query deep organizational data. By using the Model Context Protocol, the server communicates its capabilities to the AI agent, ensuring that every request for lead data is structured correctly and contextually aware.

*   **Firmographic Intelligence:** Retrieve real-time data including company size, revenue brackets, headquarters location, and industry classification.
*   **Technographic Mapping:** Identify the current software stack of a target lead (e.g., Cloud providers, CRM usage, frontend frameworks) to tailor outbound engineering or sales scripts.
*   **Intent Signals:** Access low-latency signals indicating organizational shifts or technology adoption trends.
*   **Hallucination Prevention:** All tool parameters are defined using **Zod annotations**, forcing the LLM to provide valid domain names or emails, drastically reducing "hallucinated" data requests.
*   **Confidence Scoring:** Every enrichment includes a `confidenceScore`, allowing your agent to programmatically decide if the data quality meets your workflow's threshold.

## IDE Configuration
To enable these tools in Cursor, VS Code (via the MCP extension), or Claude Desktop, add the following configuration to your `mcpServers` settings file.

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-http",
        "--url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "LEAD_ENRICHMENT_API_KEY": "YOUR_ACTUAL_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
When your AI agent calls the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This ensures that the agent can immediately use the data for downstream tasks like generating personalized emails or populating a CRM.

```json
{
  "tool_use": "enrich_lead",
  "result": {
    "status": "success",
    "data": {
      "companyName": "Acme Corp",
      "domain": "acme.com",
      "industry": "Enterprise SaaS",
      "employeeCount": 1250,
      "technographics": ["AWS", "Salesforce", "React", "Snowflake"],
      "intentSignals": ["Cloud Migration", "Series C Funding"],
      "confidenceScore": 0.98
    },
    "billing": "1 unit (Confidence > 0.6)"
  }
}
```

## The Risk-Free Value Proposition
Modern AI workflows require predictable costs. This MCP server utilizes a **Risk-Free Metered Billing** structure. Unlike traditional APIs that charge for every request, this server only bills for successful enrichments that return a `confidenceScore` greater than 0.6. If the data is low-quality, the result is unavailable, or the confidence is too low for reliable automation, the cost is exactly $0. This allows developers to build high-volume SDR swarms and lead-gen bots without the risk of burning budget on "not found" results or LLM retries.

## Get Started with the B2B Lead Enrichment MCP API
Ready to upgrade your AI agent's firmographic capabilities? Visit **[lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)** to generate your API key and access the free tier instantly.