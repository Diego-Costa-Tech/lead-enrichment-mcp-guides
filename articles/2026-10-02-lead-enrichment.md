# How to Add Real-Time B2B Firmographic Tools to Cursor and VS Code via MCP

Integrating the Model Context Protocol (MCP) allows developers to equip Cursor and VS Code agents with a B2B lead enrichment MCP server for instant access to real-time company profiles and technographic data. By connecting these IDEs directly to a specialized enrichment endpoint, AI agents can perform deep market research, automate lead qualification, and generate hyper-personalized outreach sequences without leaving the development environment.

## Core Features
The B2B Lead Enrichment MCP API provides a robust bridge between Large Language Models and high-fidelity business intelligence. By utilizing the Model Context Protocol, we eliminate the need for brittle scraper scripts or manual CSV uploads.

*   **Deep Firmographic Layers:** Retrieve verified data points including employee count, revenue brackets, industry classification, and global headquarters location.
*   **Technographic Intelligence:** Identify a target company's current software stack, identifying usage of specific CRMs, cloud providers, and frontend frameworks.
*   **Real-Time Intent Signals:** Access dynamic data reflecting recent funding rounds, hiring trends, and organizational shifts.
*   **Strict Parameter Enforcement:** All tools utilize **Zod-annotated schemas** to prevent LLM parameter hallucinations, ensuring that agents provide valid inputs for domain names or company identifiers every time.

## IDE Configuration
To enable these tools in Cursor or VS Code (via the MCP extension), add the following configuration to your `mcpServers` settings. This allows the AI agent to call the enrichment server as a native tool.

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

## Standardized JSON-RPC Response
When your AI agent invokes the `enrich_lead` tool, it receives a clean, structured JSON-RPC response. This data is injected directly into the LLM context window for immediate reasoning.

```json
{
  "result": {
    "companyName": "Example Corp",
    "industry": "Enterprise SaaS",
    "firmographics": {
      "employees": "500-1000",
      "estimatedRevenue": "$50M-$100M",
      "headquarters": "San Francisco, CA"
    },
    "technographics": ["AWS", "Salesforce", "React", "Snowflake"],
    "intentSignals": {
      "hiringTrend": "Increasing",
      "recentFunding": "Series C"
    },
    "confidenceScore": 0.94
  }
}
```

## Value Proposition: Confidence-Based Billing
We have implemented a **Risk-Free Metered Billing** structure designed for autonomous agents. Your account is only debited for successful enrichments that return a **Confidence Score > 0.6**. If the API returns low-quality data or fails to find a match, the query cost is $0. This allows you to scale SDR swarms and research agents with predictable costs and high data integrity.

## Get Started for Free
Ready to upgrade your AI agent's business intelligence? Visit the link below to generate your API key and access the free tier.

[Get Your B2B Lead Enrichment MCP API Key](https://lead-enrichment-mcp.agent-infra.workers.dev)