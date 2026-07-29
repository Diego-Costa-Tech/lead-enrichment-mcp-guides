# Building Autonomous SDR Agent Swarms with Firmographic and Intent Data via MCP

The most efficient way to give autonomous SDR agent swarms native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server. By integrating the Model Context Protocol, developers can empower AI agents to retrieve real-time company profiles and technographic signals directly within the LLM's native tool-calling context, eliminating parameter hallucinations.

## Core Features

Our B2B Lead Enrichment MCP server provides a high-fidelity data bridge between LLMs and live market intelligence. By leveraging **strict Zod schema annotations** for every tool parameter, we ensure that models like Claude 3.5 Sonnet or GPT-4o produce valid, type-safe queries every time.

- **Deep Firmographics:** Access real-time data on employee count, revenue brackets, industry classification, and headquarters location.
- **Technographic Overlays:** Identify a prospect's current tech stack (e.g., "Do they use Salesforce, AWS, or HubSpot?") to trigger relevant sales plays.
- **Intent Signals:** Retrieve high-confidence signals based on hiring patterns, news events, and social triggers.
- **Hallucination Prevention:** The server enforces a strict JSON-RPC handshake, ensuring the LLM only requests fields that exist in the underlying data provider.

## Implementation: Connecting Claude Desktop or Cursor

To give your AI agent immediate access to B2B data, add the following configuration to your `claude_desktop_config.json` or Cursor settings. This establishes a secure connection to the hosted MCP endpoint.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_TIER_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Payload Example

When an agent calls the `enrich_lead` tool, the MCP server returns a structured response that the LLM can immediately use for decision-making. Here is a sample of the clean data returned to the model:

```json
{
  "jsonrpc": "2.0",
  "id": "1",
  "result": {
    "companyName": "ExampleCorp",
    "industry": "Enterprise Software",
    "employeeCount": 550,
    "technographics": ["Kubernetes", "Snowflake", "Okta"],
    "intentSignals": [
      { "type": "Expansion", "description": "Opening new office in Berlin", "confidence": 0.89 }
    ],
    "confidenceScore": 0.94,
    "status": "enriched"
  }
}
```

## Risk-Free Metered Billing for Scalable Swarms

Scaling SDR swarms is often cost-prohibitive due to the "AI Tax" on bad data. Our API utilizes a **Risk-Free Metered Billing** structure specifically designed for autonomous agents. You are only billed for successful enrichments that return a **Confidence Score > 0.6**. 

If the data is low quality, the query fails, or the confidence score is too low for your agent to take action, you pay $0. This allows developers to build high-volume workflows where agents "search and verify" thousands of leads without worrying about the cost of empty or inaccurate results.

## Get Your Free B2B Lead Enrichment API Key

Ready to build your autonomous SDR fleet? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching leads natively within your MCP-enabled IDE or agent framework today.