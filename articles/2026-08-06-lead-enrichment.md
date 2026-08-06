# How to Connect Claude Desktop to a Live B2B Lead Enrichment MCP API

The most efficient way to provide LLMs with native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native B2B lead enrichment MCP server. By configuring your Claude Desktop or Cursor environment to interface with this protocol, you eliminate the need for manual data scraping and empower your agents to perform real-time lead qualification directly within the chat interface.

## Core Features and Technical Implementation
Our **B2B lead enrichment MCP server** provides an abstraction layer over raw firmographic data, ensuring your agents operate on the highest quality intelligence. Each tool is defined with strict **Zod annotations**, which prevents common LLM parameter hallucinations by enforcing rigid data types and validation logic before a request ever hits our API.

The system provides three primary data layers:
*   **Firmographics:** Real-time company profiles, including headquarters, headcount, and revenue estimates.
*   **Technographics:** Deep insights into the current tech stack and SaaS ecosystem of the target accounts.
*   **Intent Signals:** Proprietary scoring based on market-wide buying intent and recent company activity.

## Configuration for Claude Desktop
To integrate the service, add the following configuration to your `claude_desktop_config.json` (or your Cursor MCP settings):

```json
{
  "mcpServers": {
    "lead-enrichment": {
      "command": "npx",
      "args": ["-y", "@mcp-tools/lead-enrichment-proxy"],
      "env": {
        "MCP_API_URL": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp",
        "API_KEY": "your_api_key_here"
      }
    }
  }
}
```

## JSON-RPC Response Structure
When your agent invokes the `enrich_lead` tool, the server returns a deterministic JSON-RPC response. This structure is optimized for LLM context windows, stripping away noise while maintaining critical data points:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "TechCorp Solutions",
    "industry": "Cloud Infrastructure",
    "technographics": ["Kubernetes", "AWS", "Datadog"],
    "intentSignals": {
      "score": 88,
      "category": "High Interest"
    },
    "confidenceScore": 0.92,
    "location": "San Francisco, CA"
  },
  "id": 1
}
```

## Risk-Free Metered Billing
We prioritize developer ROI by implementing a **Confidence-Based Billing Model**. You are only charged for successful enrichments where the `confidenceScore` exceeds 0.6. Any data points returned with a confidence level below this threshold are provided at zero cost to ensure your autonomous agent swarms remain budget-efficient and highly performant.

## Get Your API Key
Ready to upgrade your agent's prospect data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start building with our MCP-native tools on the free tier today.