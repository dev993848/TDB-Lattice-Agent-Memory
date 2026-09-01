# TDB-Lattice-Agent-Memory

**Graph-native memory for AI agents.**
**Fork of TencentDB Agent Memory with LatticeDB storage backend and jsonmd support.**

---

## 🧠 What is this?

**TDB-Lattice-Agent-Memory** is an independent open-source project that reimagines AI agent memory with **LatticeDB** — a single embedded database that combines **graph, vector, and full-text search** in one file.

It is a **fork of TencentDB Agent Memory**, replacing SQLite with LatticeDB as the search projection layer while keeping TencentDB's proven L0-L3 memory architecture, ACL, MCP-server, and MemoryHub panel.

---

## 🚀 Key Features

| Feature | How it works |
| :--- | :--- |
| **Graph-native relationships** | LatticeDB stores explicit links between documents, code, and decisions. Graph traversal is **microsecond-fast** (9 µs per edge). |
| **Hybrid search** | BM25 + vector embeddings + RRF fusion — **0.83 ms** for 10-NN among 1M vectors. |
| **jsonmd documents** | Markdown content with JSON metadata + explicit `relationships`. Perfect for ADR, specs, changelogs, and plans. |
| **Single file per project** | No external Qdrant, Postgres, or Neo4j. Everything in one `.db` file. |
| **Memory layers (L0–L3)** | Inherited from TencentDB: raw conversations → atomic facts → scenarios → persona. |
| **ACL & visibility** | `private` / `team` / `restricted` — SQLite remains the source of truth for access control. |
| **MCP-server ready** | Works with OpenCode, OpenClaw, Claude Desktop, Cursor, and any MCP-compatible agent. |

---

## 🏗️ Architecture

```mermaid
flowchart LR
    A[JSONMD documents] --> B[SQLite]
    A --> C[LatticeDB]
    B --> D[ACL / Audit / Versions]
    C --> E[Graph / Vectors / BM25]
    F[Agent] --> G[MCP-server]
    G --> H[MemoryHub]
    H --> B
    H --> C
