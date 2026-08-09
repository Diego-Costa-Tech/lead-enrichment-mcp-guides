# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server. By integrating a B2B lead enrichment MCP server directly into your IDE, you allow AI agents to retrieve real-time company profiles and technographic stacks using standardized, type-safe protocols.

## Core Features
The **B2B Lead Enrichment MCP API** provides a robust interface for AI agents to query the global business landscape. To prevent the common issue of LLM parameter hallucinations, all tool definitions utilize **strict Zod annotations**, ensuring the model provides valid domains and email formats before the request is even sent.

*   **Firmographic Depth:** Instant access to company size, revenue brackets, industry classifications, and headquarters metadata.
*   **Technographic Profiling:** Identify the software stack of any lead, including CRM usage, cloud providers, and frontend frameworks.
*   **Intent & Growth Signals:** Detect hiring surges, recent funding rounds, and technology migrations.
*   **Zero-Latency Context:** Designed for the Model Context Protocol (MCP), allowing tools to be injected directly into the LLM's context window without high-latency RAG pipelines.

## Cursor and VS Code Configuration
To enable these B2B tools in Cursor or VS Code (via the MCP extension), add the following configuration to your `mcpServers` JSON settings. This connects your environment to the production-ready endpoint.

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
        "ENRICHMENT_API_KEY": "YOUR_PROVIDED_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
The server returns a structured JSON-RPC response that is optimized for LLM consumption. Below is an example of the payload returned by the `enrich_lead` tool when identifying a target organization:

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Vercel",
          "industry": "Cloud Computing",
          "technographics": ["Next.js", "React", "Tailwind CSS", "PostgreSQL"],
          "intentSignals": ["Expanding Enterprise Sales Team", "Increased AI infrastructure spend"],
          "confidenceScore": 0.96,
          "employeeCount": "500-1000"
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing
Engineering cost-effective AI workflows requires predictable pricing. This MCP server utilizes a **Risk-Free Metered Billing** structure. Your API balance is only affected when a query returns a **Confidence Score > 0.6**. If the data is low-quality, the lead is not found, or the confidence threshold isn't met, the request is billed at $0. This ensures you can build autonomous SDR swarms and data-driven agents that only pay for high-fidelity intelligence.

## Get Your B2B Lead Enrichment API Key
Start building high-context sales agents and firmographic-aware tools in minutes. Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab an API key on the free tier and connect it to your MCP-compatible environment.