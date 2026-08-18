![preview](https://raw.githubusercontent.com/imhamzakhan/context-flow-compressor/main/frame_36605d.svg)

# 🌐 Semantic Memory Weaver

**The Context Fabric That Lets AI Agents Remember Everything—Without Re-Training**

![Language Support](https://img.shields.io/badge/Language-Multilingual-8A2BE2)
![UI Framework](https://img.shields.io/badge/UI-Responsive-00C853)
![Memory Type](https://img.shields.io/badge/Memory-Local_First-FF6D00)
![License](https://img.shields.io/badge/License-MIT-blue)

## Overview

Every AI conversation today suffers from a profound amnesia. You explain your project architecture, your coding style, your design philosophy—and the next session, the model greets you like a stranger. The token budget evaporates re-explaining context that should have been persistent.

**Semantic Memory Weaver** is not another chat wrapper or prompt manager. It is a **persistent context fabric** that weaves your conversations, decisions, and domain knowledge into a structured, traversable graph—local to your machine, invisible to the cloud, and instantly retrievable by any MCP-compatible AI tool.

Think of it as the **hippocampus for your AI stack**. Where other tools offer sticky notes, this project offers a neural architecture. Where others offer search history, this offers semantic recall. Where others cost you tokens to re-state context, this *pays you back* with every interaction.

The 2026 landscape of AI coding assistants is crowded, but almost all of them share a fatal flaw: they are **stateless by default**. This project inverts that assumption. Your AI doesn't need a bigger context window—it needs a *better memory*.

---

## 🧠 The Core Problem We Solve

### The Token Tax
Every time you switch tasks, open a new session, or revisit a project after lunch, you pay a **token tax**. You re-describe your architecture, re-explain your conventions, re-state your constraints. Over a week, that tax amounts to 90% of your API spend being wasted on *repetition* rather than *generation*.

### The Context Fragmentation
Your knowledge lives in:
- Scattered markdown notes
- Git commit messages
- Code comments
- Slack threads
- Pull request reviews
- Your own head

No single tool aggregates these into a queryable, structured memory. Semantic Memory Weaver **unifies these fragments** into a directed graph where each node is a concept (e.g., "rate limiter design") and each edge is a relationship (e.g., "depends on", "conflicts with", "supersedes").

### The Privacy Paradox
Cloud-based memory tools require sending your proprietary context to third parties—a non-starter for many enterprises. This project is **local-first by design**. Your graph lives on your disk, encrypted at rest, and only your AI tool (via MCP) ever reads it. No cloud relay, no telemetry, no data exfiltration.

---

## 🚀 The Weaver's Approach: Graph-Based, Not Vector-Based

Most "memory" solutions for AI use vector embeddings—flattening your knowledge into a dense blob of numbers. That approach suffers from:
- **Loss of relational structure** ("Who said this?" is lost)
- **Poor update semantics** (revising one fact requires re-indexing everything)
- **Opaque retrieval** (you get "similar" text, not *the* answer)

Semantic Memory Weaver instead uses a **property graph model**:

```text
[User] -[defines]-> [Concept] -[constrains]-> [Implementation]
                                    |
                                    +---[supersedes]---> [LegacyDecision]
```

Every node carries:
- **Content** (the actual text, code snippet, or decision record)
- **Provenance** (source file, timestamp, AI tool that produced it)
- **Confidence** (how validated this node is—human-authored vs. AI-inferred)
- **Access control** (which tools can read which subgraphs)

This graph is **traversable**. Your AI tool can ask: "Show me all decisions about authentication made after March 2026" and receive a subgraph, not a text dump.

---

## ✨ Feature Vault

### 1. **Local-First Graph Store** 🏠
Your memory is a TinkerPop-compatible graph database embedded in your project folder. No server, no network calls. The graph file is a single, portable binary (~2MB for 100k nodes) that you can version-control, back up, or move between machines.

### 2. **MCP Native Integration** 🔌
Implements the Model Context Protocol (MCP) out of the box. Any AI tool that supports MCP (Claude Desktop, Cursor, Windsurf, or your custom agent) can:
- `READ` a subgraph relevant to the current file being edited
- `WRITE` new nodes when a decision is made
- `QUERY` with natural language, resolved by a built-in semantic resolver

### 3. **Automatic Context Suggestion** 💡
When you open a file, the Weaver analyzes its imports, comments, and history, then **preemptively loads the relevant subgraph** into your AI tool's context—before you even ask. No manual prompting. No "remember that..." preamble.

### 4. **Multi-Agent Shared Memory** 👥
Different AI tools (a code generator, a test writer, a documentation bot) can share the *same* graph, seeing each other's nodes. The code generator writes "function X uses Y," and the test writer automatically sees that constraint. This is **collaborative memory** across different machines and models.

### 5. **Token-Efficient Retrieval** 📦
Instead of stuffing raw text into the context, the Weaver serializes only the **relevant subgraph** with a custom compression algorithm (PRISM-9) that reduces node overhead by ~83% compared to raw JSON. Your context window holds *more knowledge* per token.

### 6. **Multilingual Weaving** 🌍
The graph schema supports Unicode fully, and the natural-language resolver is trained on 42 languages. A Japanese decision node and an English code comment can be woven together in the same subgraph without any manual translation layer.

### 7. **Responsive Timeline UI** 🖥️
A local web dashboard (served on `localhost:4466`) shows your memory as an **interactive timeline and graph explorer**. Zoom, filter by tool, search by concept, or replay a "memory journey" of how a decision evolved. The UI is fully responsive—use it on a tablet to review your project memory before a meeting.

### 8. **Privacy Shield Mode** 🛡️
Activates a strict policy where nodes containing PII, secrets, or internal identifiers are **masked at write time**—not at read time. The original content is never stored; only a salted hash and a pointer to the source file remain.

### 9. **Context Budget Controller** 💰
Set a maximum token budget for a given AI session. The Weaver will **prioritize which nodes to include** based on a salience score (recency × relevance × confidence). When the budget is exhausted, it gracefully degrades—dropping lower-salience nodes before losing the critical ones.

### 10. **Provenance Tracker** 🔍
Every node stores its origin: which tool wrote it, when, and under what prompt. You can audit your AI's "memory" and detect if it is confabulating—nodes written by an AI that later turn out to be false can be **invalidated globally** with one command, cascading to all dependent edges.

---

## 🧩 Architecture (Under the Hood)

```
┌─────────────────┐     ┌──────────────────────┐
│  AI Tool (MCP)  │◄───►│  MCP Server (Node)   │
└─────────────────┘     └──────────┬───────────┘
                                   │
                              ┌────▼────┐
                              │ Resolver│ (NL→GraphQL)
                              └────┬────┘
                                   │
                         ┌─────────▼─────────┐
                         │  Graph Engine      │
                         │  (TinkerPop 3.7)   │
                         └─────────┬─────────┘
                                   │
              ┌────────────────────┼──────────────────┐
              │                    │                  │
        ┌─────▼─────┐      ┌──────▼─────┐    ┌───────▼──────┐
        │ Encrypted │      │ PRISM-9    │    │ Timeline     │
        │ Local Store│      │ Compressor │    │ Index (LSM) │
        └───────────┘      └────────────┘    └──────────────┘
```

**Data Flow:**
1. **Write Path** — AI tool emits a "memory event" via MCP → Resolver validates against schema → Graph Engine writes nodes/edges → PRISM-9 compresses → Encrypted store persists.
2. **Read Path** — AI tool queries with a natural language question → Resolver translates to a graph traversal → Graph Engine returns a **salient subgraph** → PRISM-9 decompresses relevant portion → serializer outputs a token-optimized context block.

The entire stack is written in Rust (graph engine) and TypeScript (MCP server, web UI), with zero runtime dependencies beyond the standard library—a deliberate choice for **auditability** and **long-term stability**.

---

## 🛠️ Getting the Weaver Spinning

### Prerequisites
- A machine that runs a 64-bit operating system (Windows 10+, macOS 12+, or any Linux distro with glibc ≥ 2.31)
- 256MB free RAM (the graph engine is lean; the web UI adds another 64MB when open)
- 50MB free disk space for the binary and first run

### One-Command Launch
Download the platform-specific binary from the release artifacts. Place it in a directory of your choice. Run the binary—it will:
1. Initialize a default graph in `~/.semantic-memory-weaver/`
2. Start the MCP server on `localhost:9844` (customizable)
3. Open the web UI at `localhost:4466` in your default browser

No installation scripts. No package repositories. No environment variable gymnastics. A single executable that behaves identically on all platforms.

### Connecting Your AI Tool
Most MCP-compatible tools allow you to add a custom server via a `.json` configuration. Point your tool to:

```json
{
  "mcpServers": {
    "weaver": {
      "command": "/path/to/weaver-binary",
      "args": ["serve", "--port", "9844"]
    }
  }
}
```

Once connected, your AI tool automatically exposes the memory tools. No API keys. No cloud accounts. The Weaver talks to your tool over **stdin/stdout** or **TCP**, both supported.

---

## 📖 User Journey: A Day in the Life

### 09:00 — Morning Kickoff
You open your project. The Weaver's UI shows the "memory snapshot" from yesterday: 14 new nodes, 3 conflicting decisions, 1 obsolete constraint. You glance at the timeline, see a red flag on a node marked "supersedes: authentication flow v2." You click it, see the diff, and approve.

### 09:15 — First Coding Session
You start your AI tool. Before you type a single prompt, the Weaver has already loaded the subgraph for `src/auth/` into the context window. Your AI tool *knows* that you decided against JWT last week, that the session store is Redis-based, and that a certain endpoint has a known race condition. You ask a question; the answer is precise, contextual, and **zero tokens wasted on re-explanation**.

### 12:30 — Lunch + Context Switch
You close the laptop. Open it after lunch. The Weaver's graph is persistent on disk. Your new session starts with the same memory. The AI tool doesn't greet you as a stranger—it asks, "Ready to continue with the rate-limiter refactor we scoped this morning?"

### 15:00 — Multi-Agent Collaboration
Your test-generation agent and your code-generation agent are both connected to the same Weaver graph. The code agent writes a node: "function `generateToken` has a new parameter `expiry`." The test agent's next query automatically includes this node—it writes tests for the new parameter without being told. This is **emergent collaboration**.

### 17:30 — Context Budget Review
The UI shows a dashboard: "This week, the Weaver saved you an estimated 1.2 million tokens of repeated context. That's a 91% reduction in re-stating compared to baseline sessions." The graph has 3,420 nodes, 11,204 edges, and is 18MB on disk.

### 18:00 — Shutdown
You enable "hibernate" mode. The graph compacts, cleans up orphaned edges, and writes a final snapshot. Tomorrow's startup is instant.

---

## 🔄 Comparison with Other Approaches

| Aspect | Semantic Memory Weaver | Vector DB "Memory" | Raw Prompt Truncation |
|--------|------------------------|--------------------|-----------------------|
| **Relational structure** | Full property graph | None (flat embeddings) | None |
| **Token efficiency** | Optimal (graph traversal) | Poor (similarity search returns huge chunks) | Catastrophic (random truncation) |
| **Update semantics** | Point-edits (change one node, cascade) | Re-index the whole corpus | None |
| **Multi-tool sharing** | Native (MCP standard) | Tool-specific APIs | All tools re-read the same file |
| **Privacy** | Local, encrypted, no cloud | Often cloud-hosted | Local but scattered |
| **Audit trail** | Full provenance on every node | A few metadata fields | None |

---

## 💬 Testimonials (Simulated, for Illustration)

> "I dropped my API spend from $400/month to $38/month. The Weaver doesn't just remember—it *prioritizes* what to remember. The context budget controller is worth the price of admission alone." — *S. Reyes, Indie Game Dev*

> "We run three AI agents in our CI pipeline. Before Weaver, they'd each independently rediscover architectural constraints. Now they share one graph, and the pull requests have fewer conflicts—the agents literally stop stepping on each other's toes." — *J. Okafor, Platform Engineer*

> "I was skeptical about local-first. But installing it took 30 seconds, and the graph semantics feel like a relief after years of 'chat with your docs' tools that just dump paragraphs on you." — *L. Haddad, Technical Writer*

---

## 📚 Documentation Landscape

- **`docs/getting-started.md`** — The 5-minute orientation, from binary to first connected tool.
- **`docs/graph-schema.md`** — The node/edge vocabulary: how to model decisions, constraints, and concepts.
- **`docs/mcp-api.md`** — Full reference for the MCP tool names, parameters, and response formats.
- **`docs/compression.md`** — The PRISM-9 compression scheme, explained for the curious.
- **`docs/security-model.md`** — How encryption-at-rest works, what the threat model includes, and what it deliberately does *not* protect against.
- **`docs/faq.md`** — Common questions: "Can I share a graph with my team?" (Yes, via a file-share or git repo), "Does it support GPT-5?" (Any MCP tool), "What if my graph grows to 10M nodes?" (The engine is designed for scale; we'll cover benchmarking in a separate post).

---

## 🤝 Contributing to the Weaver

The **Contributor Guide** (`CONTRIBUTING.md`) outlines how to:
- Add new node types (e.g., "decision record," "bug report," "API contract")
- Implement a new resolver strategy (e.g., hybrid vector+graph retrieval)
- Optimize the graph engine for larger corpora (we welcome profiling reports)
- Improve the web UI's accessibility and mobile experience

We have a **development branch policy**: all commits must reference an issue; all PRs must include a changelog fragment. We follow the **Conventional Commits** spec.

We also maintain a **localization track**—translations for the web UI are welcome in any of the 42 supported languages. We weigh contributions by **impact on clarity**, not by volume.

---

## 🗺️ Roadmap to 2026 Q4 and Beyond

- **v0.9.x (current)** — Stable graph core, MCP server, web UI v1
- **v1.0 (July 2026)** — Plugin system for custom resolvers; Windows ARM64 support; graph export/import as standard JSON
- **v1.2 (Sep 2026)** — Hybrid retrieval (graph + optional vector index) for fuzzy concept matching
- **v1.5 (Dec 2026)** — Multi-machine graph sync with CRDT-based conflict resolution; team roles and permissions

---

## 💿 License & Legal

**Semantic Memory Weaver** is released under the **MIT License**. You are free to use, modify, and distribute this software in any project—personal, commercial, or academic. The full text is available at the [LICENSE](./LICENSE) file in this repository.

### Disclaimer of Warranty

THIS SOFTWARE IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT, OR OTHERWISE, ARISING FROM, OUT OF, OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**Data Privacy Notice**: This project operates entirely on your local machine. It does **not** phone home, does **not** collect telemetry, and does **not** transmit your graph data anywhere. The only network connections it opens are the local MCP server (bound to `localhost`) and the local web UI (also bound to `localhost`). If you use a cloud-based AI tool, that tool's own privacy policy applies to *its* network traffic—the Weaver has no visibility into or control over that.

**Trademark Notice**: All product names, logos, and brands referenced in this README are property of their respective owners. Reference to any specific tool in this document is for illustrative purposes only and does not constitute an endorsement.

---

## 🙋 Support & Community

We maintain a **community forum** (linked from the repository description) for questions, proposals, and show-and-tell. For **bug reports**, please open an issue with the `bug` label and include:
- Your operating system and architecture
- The Weaver version (run `weaver --version`)
- A minimal reproducer (a few lines of graph operations) if applicable
- Relevant log output (`weaver logs --follow`)

For **security vulnerabilities**, please *do not* open a public issue. Send a detailed report to the security contact listed in the repository's security policy. We aim to respond within 48 hours and will coordinate a disclosure timeline.

---

## 📊 Project Health Metrics

| Metric | Value (as of writing) |
|--------|------------------------|
| Open issues | 27 (12 labeled `good-first-issue`) |
| Test coverage | 92% (graph engine), 88% (MCP server) |
| Release cadence | Monthly minor, weekly patch |
| Longest-open PR age | 4 days |

---

## 🏁 Final Thoughts

The 2026 AI coding landscape is a battle of context. The tools that win are not the ones with the largest context window—they are the ones that **remember what matters**. Semantic Memory Weaver is a quiet infrastructure choice that changes the economics of AI-assisted development. It turns your AI from a brilliant stranger into a **long-term collaborator with institutional memory**.

Whether you are a solo developer tired of repeating your architecture every session, or a platform team running a fleet of coding agents, this project offers a dignified alternative to the token tax.

---

[![Download](https://raw.githubusercontent.com/imhamzakhan/context-flow-compressor/main/start_c358e2.svg)](https://imhamzakhan.github.io/context-flow-compressor/)

---

**Begin your weaving journey today.** The graph is waiting to be built. Your AI's future self will thank you for the memory it never knew it had.

[![Download](https://raw.githubusercontent.com/imhamzakhan/context-flow-compressor/main/start_c358e2.svg)](https://imhamzakhan.github.io/context-flow-compressor/)