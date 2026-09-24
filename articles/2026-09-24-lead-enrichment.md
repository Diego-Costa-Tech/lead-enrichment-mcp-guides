# How to Give Cursor and VS Code Copilot Live Firmographic Tools via MCP

The most efficient way to give LLMs native access to live B2B firmographics and intent data without custom middleware is by deploying an MCP-native B2B lead enrichment MCP server directly into your IDE. By utilizing the Model Context Protocol, developers can now equip their local AI agents with real-time company profiles and technographic data, ensuring high-fidelity outputs for sales and research workflows.

## Core Features
Our B2B lead enrichment MCP server provides high-density data payloads that are pre-structured for LLM consumption. Key technical highlights include:
*   **Firmographic Intelligence:** Access real-time **companyName**, **industry**, **employeeCount**, and **annualRevenue** mapping.
*   **Technographic Stack:** Deep insights into the current tech stack, including **CRM integration**, **cloud infrastructure**, and **marketing automation tools**.
*   **Predictive Intent Signals:** Normalized scores representing buying propensity.
*   **Hallucination Mitigation:** All tool parameters utilize strict **Zod annotations**, forcing the LLM to adhere to schema constraints for `domain` or `company_name` inputs, preventing common parameter hallucination issues.

## Configuring Cursor / VS Code Copilot
To integrate the API into your environment, add the following configuration to your `mcp.json` settings file. This links the Claude-compatible MCP server to your local agentic tools:

```json
{
  "mcpServers": {
    "b2b-lead-enrichment": {
      "command": "npx",
      "args": [
        "-y",
        "@agent-infra/lead-enrichment-mcp"
      ],
      "env": {
        "API_KEY": "your_api_key_here",
        "ENDPOINT": "https://lead-enrichment-mcp.agent-infra.workers.dev/mcp"
      }
    }
  }
}
```

## JSON-RPC Response Example
When an LLM calls the `enrich_lead` tool, the server returns a clean, sanitized JSON-RPC response. This structure ensures your agent processes only valid, high-confidence data:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "companyName": "Acme Corp",
    "industry": "SaaS",
    "technographics": ["Salesforce", "AWS", "HubSpot"],
    "intentSignals": {
      "marketPulse": 0.89,
      "buyingStage": "researching"
    },
    "confidenceScore": 0.94
  },
  "id": 1
}
```

## The Value Proposition: Risk-Free Metered Billing
We prioritize developer ROI by implementing a **Risk-Free Metered Billing** structure. You are exclusively billed for successful enrichments where the **Confidence Score > 0.6**. If the API returns low-quality data or fails to find a match, the query costs $0, ensuring your autonomous SDR swarms remain cost-effective while scaling.

## Get Started Today
Ready to arm your AI agents with enterprise-grade data? Visit [lead-enrichment-mcp.agent-infra.workers.dev](https://lead-enrichment-mcp.agent-infra.workers.dev) to generate your API key and start with our generous free tier today.