# How to Give Cursor and VS Code Copilot Live B2B Firmographic Tools

Integrating live B2B firmographic data into your IDE via the Model Context Protocol (MCP) allows AI agents like Cursor to perform real-time lead qualification and company research without leaving your codebase. By connecting to a dedicated B2B lead enrichment MCP server, you eliminate LLM hallucinations and manual data entry by providing your assistant with a direct, schema-validated pipeline to fresh intent and technographic signals.

## Core Features of the Enrichment MCP
The B2B Lead Enrichment MCP API provides a structured interface for AI models to query deep organizational data. Unlike generic web search tools, this server uses strict **Zod-annotated parameters** to ensure that models like Claude 3.5 Sonnet or GPT-4o accurately map input fields to query parameters, drastically reducing the risk of parameter hallucinations.

- **Firmographic Intelligence:** Real-time access to headcount, revenue brackets, and industry classifications.
- **Technographic Mapping:** Identification of a target company’s software stack, including CRM, cloud providers, and analytics tools.
- **Dynamic Intent Signals:** Live data on hiring surges, recent funding rounds, and executive transitions.
- **Confidence Scoring:** Every response includes a precision metric, allowing autonomous agents to make data-driven decisions on whether to proceed with a lead.

## Integration Config for Cursor & Claude Desktop
To enable these tools, add the following configuration to your MCP settings file (typically found in `~/Library/Application Support/Claude/claude_desktop_config.json` for Claude or the MCP settings pane in Cursor).

```json
{
  "mcpServers": {
    "b2b-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/mcp-server-lead-enrichment",
        "--api-url",
        "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      ],
      "env": {
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY_HERE"
      }
    }
  }
}
```

## Real-Time JSON-RPC Response Payload
When your AI assistant invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This structure is optimized for LLM token efficiency, providing maximum context with minimal overhead.

```json
{
  "tool": "enrich_lead",
  "parameters": { "domain": "stripe.com" },
  "response": {
    "companyName": "Stripe, Inc.",
    "industry": "Fintech / Payments",
    "employeeCount": 8000,
    "technographics": ["AWS", "React", "Ruby on Rails", "Salesforce"],
    "intentSignals": {
      "hiring": "High (Engineering & Sales focus)",
      "recentNews": "Expansion into Southeast Asian markets"
    },
    "confidenceScore": 0.98,
    "status": "success"
  }
}
```

## Risk-Free Metered Billing Architecture
One of the most significant barriers to scaling AI SDR swarms is the cost of low-quality data. This MCP server implements a **Confidence-First Billing** model. Your account is only debited for enrichments that return a `confidenceScore` higher than 0.6. If the data is stale, the domain is unreachable, or the enrichment provides low-utility signals, the query cost is $0. This allows developers to build high-volume, autonomous workflows that are both cost-effective and highly reliable.

## Get Your Free B2B Enrichment API Key
Ready to upgrade your AI agent's research capabilities? Stop relying on outdated training data and give your LLM live access to the B2B landscape.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your free API key and start enriching leads natively within your MCP-enabled workflow today.**