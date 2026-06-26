# Cross-Protocol Governance & Security Checklist

Agent protocols solve routing, not governance. Before deploying a mixed A2A/MCP stack to production, ensure your architecture passes these security and auditability checks. 

## 1. Identity Persistence
- [ ] **Token Injection:** Does your system actively inject original user identity tokens into all protocol payloads?
- [ ] **Cross-Protocol Tracking:** When an agent switches from A2A (messaging a peer) to MCP (executing a tool), does the human user's core permission context persist?
- [ ] **Audit Stitching:** Is there a centralized logging gateway that stitches A2A orchestration logs and MCP execution logs into a single, unified audit trail?

## 2. Mitigating the Confused Deputy Vulnerability
- [ ] **Public vs. Internal Isolation:** Are public-facing agents physically/logically prevented from executing high-privilege MCP tool calls directly?
- [ ] **Intent Validation:** When an internal agent receives an A2A request from another agent, does a gateway explicitly validate the authorization of the *original requester* before fulfilling it?
- [ ] **Gateway SSO & RBAC:** Is MCP access strictly governed by an SSO/RBAC gateway rather than trusting the agent by default?

## 3. Lock-In & Reversibility
- [ ] **Payload Decoupling:** Are your proprietary agents decoupled from underlying communication standards via a translation gateway?
- [ ] **Standardization Readiness:** If the broader market abandons your currently implemented standard (e.g., within the next 18 months), can you swap it out at the gateway level without a complete platform rewrite?
