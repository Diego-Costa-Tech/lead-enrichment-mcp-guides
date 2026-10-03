# How to Connect Cursor and VS Code to a Live B2B Lead Enrichment MCP API

Integrating a B2B lead enrichment MCP server allows AI agents like Cursor and VS Code Copilot to fetch real-time company profiles and technical signals natively using the Model Context Protocol. By connecting your IDE to a live enrichment tool, you eliminate LLM parameter hallucinations and provide your coding assistants with the high-fidelity firmographic data needed to build personalized sales automation or account-based marketing (ABM) logic.

## Core Features
The B2B Lead Enrichment MCP server provides deep integration into the AI agent workflow by exposing structured tools for data retrieval. Unlike standard REST APIs that require manual prompt engineering, this MCP-native server uses strict **Zod-annotated parameters** to ensure the LLM passes valid domain names and entity identifiers.

*   **Real-time Firmographics:** Access up-to-date employee counts, revenue brackets, and HQ locations directly within the chat interface.
*   **Technographic Mapping:** Identify the software stack and infrastructure (e.g., AWS vs Azure, React vs Vue) of a target lead to tailor technical outreach.
*   **Intent Signal Processing:** Retrieve active buying signals and recent funding data to prioritize high-value prospects.
*   **Hallucination Prevention:** By leveraging the MCP `tools/call` framework, the LLM is forced to use verified external data rather than guessing company details from its training weights.

## Configuration for Cursor or Claude Desktop
To give your IDE or Claude Desktop client native access to live B2B data, add the following configuration to your MCP settings file (typically `cursor-settings.json` or `claude_desktop_config.json`).

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

## Standardized JSON-RPC Response Example
When you trigger the `enrich_lead` tool, the MCP server returns a clean, structured payload. This allows the LLM to parse the `confidenceScore` and `intentSignals` to determine the next step in your SDR agent's logic.

```json
{
  "method": "tools/call",
  "params": {
    "name": "enrich_lead",
    "arguments": {
      "domain": "example-startup.io"
    }
  },
  "result": {
    "content": [
      {
        "type": "text",
        "text": {
          "companyName": "ExampleTech",
          "industry": "Cloud Infrastructure",
          "technographics": ["Kubernetes", "Terraform", "Stripe"],
          "intentSignals": ["Series B Funding", "Expanding DevRel Team"],
          "confidenceScore": 0.94,
          "isHighQuality": true
        }
      }
    ]
  }
}
```

## Risk-Free Metered Billing for AI Workflows
Building autonomous agents can be expensive if you are billed for every API call, regardless of data quality. This MCP server utilizes a **Risk-Free Metered Billing** structure. Your account is only debited for successful enrichments where the **Confidence Score is > 0.6**. If the server returns low-quality data or cannot find the lead, the query cost is $0. This allows developers to scale "SDR Swarms" and automated outreach pipelines without worrying about burning credits on "Not Found" responses.

## Get Your Free API Key
Ready to upgrade your AI agent's B2B intelligence? Visit the developer portal to grab an API key and start enriching leads with the Model Context Protocol today.

[Get Your Free API Key at lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev)