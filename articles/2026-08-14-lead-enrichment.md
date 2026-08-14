# Supercharging Cursor and VS Code with Live B2B Lead Enrichment via MCP

Integrating a native Model Context Protocol (MCP) server allows developers to provide LLMs like Cursor and VS Code Copilot with real-time access to B2B firmographics and intent data without writing custom API glue code. By connecting to the B2B Lead Enrichment MCP API, your AI agents can instantly resolve company profiles, technographic stacks, and buying signals directly within your IDE workflow.

## Core Features
The B2B Lead Enrichment MCP server exposes deep data layers to your AI tools using a standardized protocol. This isn't just a basic scraper; it provides high-fidelity **Firmographic** (revenue, headcount, HQ location), **Technographic** (installed software, cloud providers), and **Intent Signals** (recent funding, hiring trends) via a single tool call. To ensure production reliability, every tool parameter is defined with strict **Zod annotations**, which virtually eliminates LLM parameter hallucinations by forcing the model to adhere to the required JSON schema for domain names and entity lookups.

## IDE Configuration
To give Cursor or VS Code native access to this data, add the following configuration to your MCP settings. This uses the hosted server endpoint to fetch live data directly into your chat or agentic workflow.

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
        "ENRICHMENT_API_KEY": "YOUR_FREE_API_KEY"
      }
    }
  }
}
```

## JSON-RPC Response Example
When you ask an agent to "Research the tech stack of stripe.com," the MCP server returns a clean, structured JSON-RPC response. This allows the LLM to process hard data rather than guessing.

```json
{
  "tool": "enrich_lead",
  "response": {
    "companyName": "Stripe",
    "industry": "FinTech / Software",
    "headcount": "7000+",
    "technographics": ["AWS", "React", "Ruby on Rails", "Kubernetes", "Salesforce"],
    "intentSignals": {
      "hiring": ["High", "Engineering", "Compliance"],
      "recentFunding": "Series I",
      "growthScore": 0.94
    },
    "confidenceScore": 0.98,
    "source": "verified_firmographic_index"
  }
}
```

## The Value Proposition: Risk-Free Metered Billing
Unlike traditional SaaS APIs that charge for every request (including "not found" or low-quality results), this B2B Lead Enrichment MCP API utilizes a **Risk-Free Metered Billing** structure. Developers are only billed for successful enrichments that return a **Confidence Score > 0.6**. If the database cannot verify the company or the data quality is low, the query costs exactly $0. This allows you to build cost-effective AI SDR swarms and autonomous agents that can iterate through thousands of leads without wasting budget on "hallucinated" or empty data points.

## Get Started with a Free API Key
Ready to upgrade your AI agent's knowledge base with live B2B data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to grab your API key on the free tier and start enriching leads directly in Cursor, VS Code, or Claude Desktop.