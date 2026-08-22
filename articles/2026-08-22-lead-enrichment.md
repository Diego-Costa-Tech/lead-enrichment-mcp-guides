# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give AI agents like Cursor or VS Code Copilot native access to live B2B firmographics and intent data is by connecting them to a dedicated Model Context Protocol (MCP) server. By integrating the B2B Lead Enrichment MCP API, developers can eliminate manual data lookups and provide their LLMs with a real-time toolset for identifying company profiles and technographic stacks directly within the IDE.

## Core Features
The B2B Lead Enrichment MCP server provides a high-fidelity data layer designed specifically for LLM consumption. Unlike standard REST APIs that return messy HTML or unstructured text, this MCP server utilizes **strict Zod-schema annotations** to define parameters, which drastically reduces LLM parameter hallucinations during tool calls. 

Key data layers include:
*   **Deep Firmographics:** Access real-time data on company size, revenue brackets, headquarters location, and industry classification.
*   **Technographic Intelligence:** Identify the software stack a lead is currently using (e.g., AWS, Salesforce, HubSpot) to tailor outreach or technical integration advice.
*   **Intent Signals & Buying Power:** Extract signals that indicate a company is in a buying cycle or expanding their technical infrastructure.
*   **Confidence Scoring:** Every response includes a precision metric, ensuring your agent only acts on high-certainty data.

## Cursor and VS Code Configuration
To enable these tools in Cursor or any MCP-compliant VS Code extension, add the following configuration to your `mcpServers` settings. This points your environment to the production-ready endpoint.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## Structured JSON-RPC Response Example
When your LLM invokes the `enrich_lead` tool, it receives a clean, structured JSON object. This allows the model to reason over the data without parsing noise.

```json
{
  "method": "tools/call",
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Acme Corp",
          "industry": "Enterprise Software",
          "headcount": "500-1000",
          "technographics": ["Kubernetes", "Snowflake", "React"],
          "intentSignals": "High - Recent expansion into EMEA",
          "confidenceScore": 0.94,
          "isQualified": true
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing
Building AI workflows shouldn't be a gamble on data quality. This MCP server implements a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the server returns low-quality data or fails to find a match, the query cost is $0, allowing you to scale autonomous SDR swarms and lead-gen bots with predictable ROI.

## Get Started with a Free API Key
Ready to upgrade your AI agent's context with real-world B2B data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching leads natively in your IDE today.