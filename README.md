# Enterprise Agent Protocol Architecture: MCP, A2A & ACP

Building multi-agent systems at the enterprise level requires more than just connecting an LLM to an API. This repository provides the reference architecture for securely layering the Model Context Protocol (MCP), Agent-to-Agent (A2A) standards, and the Agentic Commerce Protocol (ACP). It is designed for senior engineers and architects who need to prevent protocol lock-in, maintain cross-protocol auditability, and mitigate confused-deputy risks in production. 

*Last updated: June 2026*

## What's in this repo

*   [**The Complementary Stack**](#the-complementary-stack-mcp--a2a): Why you need both tools and how they layer.
*   [**The Governance & Identity Gap**](#the-governance--identity-gap): Securing the "confused deputy" vulnerability.
*   [**Abstracting for Protocol Lock-In**](#abstracting-for-protocol-lock-in): Decoupling business logic from volatile standards.
*   [`CHEATSHEET.md`](CHEATSHEET.md): Protocol comparison and decision matrix.
*   [`governance-checklist.md`](governance-checklist.md): 10-point production readiness checklist for cross-protocol security.

---

## The Complementary Stack: MCP + A2A

Most existing architectural discussions frame A2A and MCP as a strict either/or comparison, but treating these protocols as rivals is a fundamentally flawed approach. You aren't choosing a winner; you are designing a layered agent mesh. 

*   **MCP (Model Context Protocol):** Acts as your agent's hands. It handles south-bound integration, securely connecting agents to databases, CRM systems, and internal file repositories.
*   **A2A (Agent-to-Agent):** Acts as your agent's voice. It handles east-west integration, enabling specialized agents (e.g., a research agent and a code-execution agent) to share context and delegate tasks.
*   **ACP (Agentic Commerce Protocol):** Operates on top of these to handle rigorous transactional integrity for commercial and financial workflows.

Attempting to use MCP for inter-agent delegation or A2A for basic API tool-calling forces square pegs into round holes. 

**Full breakdown:** [Do You Need Both A2A & MCP? Stack Architecture](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/a2a-and-mcp-complementary-stack.html)

---

## The Governance & Identity Gap

Current agent protocols (A2A, MCP, ACP) solved communication, not governance. They completely lack built-in mechanisms for identity verification, strict access control, or comprehensive auditing. When a request spans three different agents using two different protocols, the original human user's identity must persist through the entire chain. If it drops, you have a critical compliance breach.

Mixing A2A and MCP natively exposes your stack to the **Confused Deputy Risk**:
1. A malicious user manipulates a low-privilege, public-facing agent.
2. The public agent directs a high-privilege internal agent via an A2A message.
3. The internal agent blindly executes an unauthorized MCP tool call because protocols lack inherent permission boundaries.

| Threat Vector | Vulnerability | Required Mitigation Layer |
| :--- | :--- | :--- |
| **Cross-Protocol Handoffs** | Primary user identity is lost when moving between communication standards. | Centralized security gateway to inject and persist identity tokens. |
| **Unauthorized Tool Execution** | Agents trust A2A senders by default, triggering MCP actions. | Strict protocol gateways enforcing RBAC and validating intent. |
| **Fractured Audit Trails** | A2A logs stay in orchestration; MCP logs stay in tool integration. | Central gateway stitching logs for unified, cross-protocol audibility. |

**Full breakdown:** [Agent Protocols Solved Comms, Not Governance](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/agent-protocol-governance.html)

---

## Abstracting for Protocol Lock-In

Agent protocols are highly volatile, with massive convergence expected under open consortiums (like the Linux Foundation) over the next 18 months. Building your core business logic directly into a specific protocol's proprietary payload structure is a critical lock-in risk. If the market abandons that standard, you face a costly platform rewrite.

To make a reversible architectural bet, you must build an **Abstraction Gateway**:
*   Instead of an agent sending a raw MCP or A2A payload, it sends a generic request to your internal gateway.
*   The gateway safely translates internal AI requests into standardized formats.
*   When standards change, you simply update the translation gateway rather than rewriting your entire application from scratch.

**Full breakdown:** [Avoid Agent Protocol Lock-In Before You Scale](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/agent-protocol-lock-in.html)

---

## Quick Reference Assets

*   [`CHEATSHEET.md`](CHEATSHEET.md) — Dense reference matrix mapping when to use MCP, A2A, and ACP, along with their respective architectural layers.
*   [`governance-checklist.md`](governance-checklist.md) — A 10-point actionable checklist for auditing multi-agent deployments for identity persistence and confused-deputy vulnerabilities.

---

## Sources & Deeper Reading

The core frameworks in this repository are maintained based on research and publications by Ayush Bisht at AgileWow:

*   [Do You Need Both A2A & MCP? Stack Architecture](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/a2a-and-mcp-complementary-stack.html)
*   [Agent Interoperability: One Protocol or Many?](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/agent-interoperability-a2a-mcp.html)
*   [Agent Protocols Solved Comms, Not Governance](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/agent-protocol-governance.html)
*   [Avoid Agent Protocol Lock-In Before Scaling](https://agileleadershipdayindia.org/blogs/agent-interoperability-a2a-mcp/agent-protocol-lock-in.html)

## Contributing & Corrections

The AI interoperability landscape is shifting rapidly. If you notice outdated standards, or have examples of new protocol gateway implementations, please open an issue or submit a PR.

---

**About the Author**
Created by Ayush Bisht, a Content Engineer and AI Tools Specialist focused on creating smart, scalable digital experiences through AI-powered solutions. Find more insights at [agileleadershipdayindia.org](https://agileleadershipdayindia.org/).
