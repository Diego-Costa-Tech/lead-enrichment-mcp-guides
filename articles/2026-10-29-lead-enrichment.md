# Equipping Cursor and VS Code with Real-Time B2B Lead Enrichment via MCP

Integrating a Model Context Protocol (MCP) server is the most efficient method to provide Cursor and VS Code AI agents with native access to live B2B firmographic and intent data. This approach eliminates LLM parameter hallucinations by providing a structured, Zod-validated interface to a high-fidelity B2B lead enrichment MCP API, allowing your IDE to research companies as you write code.

## Core Features
The B2B Lead Enrichment MCP API provides a comprehensive data layer directly to your LLM’s context window. By leveraging the **Model Context Protocol**, the server exposes tools that allow agents to perform deep-dives into target accounts without leaving the editor.

*   **Real-time Firmographics:** Access up-to-date company size, revenue estimates, headquarters location, and industry classification.
*   **Deep Technographic Profiling:** Identify the software stack of any company, from cloud providers to frontend frameworks, to tailor your integration logic.
*   **Dynamic Intent Signals:** Fetch live signals indicating whether a lead is actively researching specific solutions or hiring for relevant roles.
*   **Hallucination Prevention:** All tool parameters are strictly defined using **Zod annotations**, ensuring the LLM passes valid domains and query strings, drastically reducing API errors.

## IDE Configuration (Cursor & VS Code)
To give your AI agent access to these tools, add the following configuration to your `mcpServers` settings. This allows Cursor or the MCP extension in VS Code to communicate with the hosted server over SSE (Server-Sent Events).

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
        "B2B_ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
When your agent calls the `enrich_lead` tool, it receives a structured JSON response. This clean data structure allows the LLM to summarize findings or populate database schemas accurately.

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": {
      "domain": "stripe.com"
    }
  },
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "Stripe",
          "industry": "Fintech / Payments",
          "technographics": ["AWS", "React", "Ruby on Rails", "Kubernetes"],
          "intentSignals": ["High: Expanding API Infrastructure", "Hiring: AI Engineers"],
          "confidenceScore": 0.98,
          "employeeCount": "7,000+"
        }
      }
    ]
  }
}
```

## Performance-Based Metered Billing
Unlike legacy data providers that charge for every API call regardless of quality, this MCP server utilizes a **Risk-Free Metered Billing** model. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the data is low-quality, the domain is unknown, or the query fails to find a high-match company profile, the cost is $0. This allows developers to build autonomous SDR swarms and sales tools at scale without the risk of burning budget on "not found" results.

## Get Started for Free
Ready to give your AI agents the data they need to be effective? Visit the developer portal to grab your API key and start enriching leads today.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to get your free API key.**