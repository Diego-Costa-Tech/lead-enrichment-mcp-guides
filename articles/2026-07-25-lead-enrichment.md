# How to Give Cursor and VS Code Copilot Live B2B Lead Enrichment MCP Tools

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native API server. By integrating this B2B lead enrichment MCP server, developers can provide Cursor, VS Code, and Claude Desktop with real-time company profiles and technographics directly via the Model Context Protocol to eliminate manual data entry in sales and engineering workflows.

## Core Features of the B2B Enrichment MCP

To bridge the gap between static LLM knowledge and the dynamic business landscape, this MCP server provides a high-fidelity data layer accessible via standard JSON-RPC calls. It is designed specifically for AI Agents (SDR swarms, research bots, and IDE extensions) to prevent parameter hallucinations through strict **Zod-schema annotations**.

*   **Deep Firmographics:** Instantly retrieve company size, revenue brackets, headquarters location, and founding dates.
*   **Live Technographics:** Identify the specific software stack a company uses (e.g., AWS, Salesforce, React, Stripe) to tailor engineering or sales outreach.
*   **Intent & Signal Detection:** Access real-time growth signals, recent funding rounds, and hiring trends that indicate high-propensity targets.
*   **Hallucination-Proof Tooling:** Every tool within the MCP server uses strictly defined input parameters, ensuring that LLMs like Claude 3.5 Sonnet or GPT-4o provide valid JSON inputs every time.

## Integration Configuration

To enable these tools in **Claude Desktop** or **Cursor**, add the following configuration to your `claude_desktop_config.json` or your MCP settings file. This points the LLM to the hosted B2B Lead Enrichment endpoint.

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

When your AI Agent invokes the `enrich_lead` tool, it receives a structured payload. This clean data structure allows the LLM to reason about a company's needs without parsing messy HTML or outdated CSVs.

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
    "companyName": "Stripe",
    "industry": "Financial Services",
    "technographics": ["AWS", "Ruby on Rails", "React", "GraphQL"],
    "intentSignals": ["Expanding European Infrastructure", "Hiring AI Engineers"],
    "confidenceScore": 0.98,
    "employeeCount": "7,000+",
    "estimatedRevenue": "$14B+"
  }
}
```

## Risk-Free Metered Billing for AI Workflows

Building autonomous SDR agents or data pipelines often leads to unpredictable costs due to LLM retries or low-quality data. This B2B Lead Enrichment MCP API solves this by implementing a **Confidence-First Billing** model. 

You are only billed for successful enrichments where the system provides a **Confidence Score > 0.6**. If the data is unavailable, low quality, or the query fails to find a match, the cost is $0. This allows developers to scale SDR swarms and firmographic research tools with complete cost certainty and zero waste on "hallucinated" or empty data points.

## Get Your Free B2B Enrichment API Key

Ready to turn your LLM into a powerful B2B research engine? You can start integrating real-time firmographics into your local IDE or AI agents in less than two minutes.

**Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier today.**