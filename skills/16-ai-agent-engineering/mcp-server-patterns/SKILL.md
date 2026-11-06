---
name: mcp-server-patterns
description: Build MCP servers with Node/TypeScript SDK — tools, resources, prompts, Zod validation, stdio vs Streamable HTTP. Use Context7 or official MCP docs for latest API. Use when building or debugging an MCP server — tools, resources, prompts, validation, or transport choice.
metadata:
  origin: ECC
version: 1.7.0
---

# Skill: Model Context Protocol (MCP) Server Engineering

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 16 — AI Agent Engineering  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `mcp-server-patterns`
- **Category**: AI Agent Engineering (Domain 16)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Build, harden, and validate MCP servers, tools, resources, and prompts using official Node/TypeScript and Python SDKs.
- **When to Use**: Building custom MCP servers, exposing tools to AI agents, integrating local APIs, or debugging MCP transports.
- **Essential Invariants**:
  1. Validate all MCP tool input parameters using strict runtime schemas (Zod / Pydantic).
  2. Handle errors gracefully; return descriptive error messages in MCP ToolResult rather than crashing server process.
  3. Enforce security boundaries: sanitize paths, prohibit arbitrary command execution, and protect secrets.
- **Minimal Workflow**:
  1. Define MCP tool contracts with clear names, descriptions, and typed parameter schemas.
  2. Implement tool handler logic with strict input validation and boundary checks.
  3. Configure transport (stdio for local agents, Streamable HTTP / SSE for remote).
  4. Author automated MCP client tests verifying tool invocation, error handling, and resource streaming.
- **Expected Deliverables**: Tested, schema-validated MCP server with passing automated tool integration tests.
- **Critical Restrictions**: Never expose unconstrained shell execution tools without strict parameter whitelisting.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

The Model Context Protocol (MCP) lets AI assistants call tools, read resources, and use prompts from your server. Use this skill when building or maintaining MCP servers. The SDK API evolves; check Context7 (query-docs for "MCP") or the official MCP documentation for current method names and signatures.

For the broader routing decision of when a capability should be a rule, a skill, MCP, or a plain CLI/API workflow, see `docs/capability-surface-selection.md`.

### When to Use

Use when: implementing a new MCP server, adding tools or resources, choosing stdio vs HTTP, upgrading the SDK, or debugging MCP registration and transport issues.

### How It Works

### Core concepts

- **Tools**: Actions the model can invoke (e.g. search, run a command). Register with `registerTool()` or `tool()` depending on SDK version.
- **Resources**: Read-only data the model can fetch (e.g. file contents, API responses). Register with `registerResource()` or `resource()`. Handlers typically receive a `uri` argument.
- **Prompts**: Reusable, parameterised prompt templates the client can surface (e.g. in Claude Desktop). Register with `registerPrompt()` or equivalent.
- **Transport**: stdio for local clients (e.g. Claude Desktop); Streamable HTTP is preferred for remote (Cursor, cloud). Legacy HTTP/SSE is for backward compatibility.

The Node/TypeScript SDK may expose `tool()` / `resource()` or `registerTool()` / `registerResource()`; the official SDK has changed over time. Always verify against the current [MCP docs](https://modelcontextprotocol.io) or Context7.

### Connecting with stdio

For local clients, create a stdio transport and pass it to your server’s connect method. The exact API varies by SDK version (e.g. constructor vs factory). See the official MCP documentation or query Context7 for "MCP stdio server" for the current pattern.

Keep server logic (tools + resources) independent of transport so you can plug in stdio or HTTP in the entrypoint.

### Remote (Streamable HTTP)

For Cursor, cloud, or other remote clients, use **Streamable HTTP** (single MCP HTTP endpoint per current spec). Support legacy HTTP/SSE only when backward compatibility is required.

### Examples

### Install and server setup

```bash
npm install @modelcontextprotocol/sdk zod
```

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { z } from "zod";

const server = new McpServer({ name: "my-server", version: "1.0.0" });
```

Register tools and resources using the API your SDK version provides: some versions use `server.tool(name, description, schema, handler)` (positional args), others use `server.tool({ name, description, inputSchema }, handler)` or `registerTool()`. Same for resources — include a `uri` in the handler when the API provides it. Check the official MCP docs or Context7 for the current `@modelcontextprotocol/sdk` signatures to avoid copy-paste errors.

Use **Zod** (or the SDK’s preferred schema format) for input validation.

### Best Practices

- **Schema first**: Define input schemas for every tool; document parameters and return shape.
- **Errors**: Return structured errors or messages the model can interpret; avoid raw stack traces.
- **Idempotency**: Prefer idempotent tools where possible so retries are safe.
- **Rate and cost**: For tools that call external APIs, consider rate limits and cost; document in the tool description.
- **Versioning**: Pin SDK version in package.json; check release notes when upgrading.

### Official SDKs and Docs

- **JavaScript/TypeScript**: `@modelcontextprotocol/sdk` (npm). Use Context7 with library name "MCP" for current registration and transport patterns.
- **Go**: Official Go SDK on GitHub (`modelcontextprotocol/go-sdk`).
- **C#**: Official C# SDK for .NET.

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
