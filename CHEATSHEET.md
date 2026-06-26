# Agent Interoperability Protocol Cheatsheet

When architecting a multi-agent system, selecting the correct protocol for the correct layer is mandatory to prevent bottlenecks and security flaws. Use this matrix to route agent traffic appropriately.

## Protocol Core Definitions

| Protocol | Primary Function | Architectural Layer | Example Use Case |
| :--- | :--- | :--- | :--- |
| **MCP** (Model Context Protocol) | South-bound tool & data integration. | Execution Layer | A Research Agent querying a secure vector database or internal CRM to read context. |
| **A2A** (Agent-to-Agent) | East-west agent communication. | Orchestration Layer | A Triage Agent handing off synthesized user requirements to a specialized Code-Execution Agent. |
| **ACP** (Agentic Commerce Protocol) | Transactional and commercial integrity. | Application / Commerce Layer | Managing financial workflows securely across different agent ecosystems. |

## Protocol Layering Rules

1. **Start with MCP:** Almost all enterprise deployments start here. You need your initial agent to perform useful work by connecting to existing enterprise tools.
2. **Scale with A2A:** Only add A2A when a single agent can no longer handle the complexity of the user's prompt, necessitating specialized multi-agent orchestration.
3. **Never Mix Unsecured:** Never allow an A2A message to directly trigger an MCP tool call without a gateway in the middle to verify intent.

## Abstraction vs. Lock-in

*   **The Risk:** Building core business logic into a specific protocol's proprietary payload.
*   **The Fix:** Deploy an internal **Abstraction Gateway**. Agents send generic requests to the gateway; the gateway translates them into MCP or A2A. This ensures architectural reversibility as industry standards consolidate over the next 18 months.
