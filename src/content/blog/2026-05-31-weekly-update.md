---
title: "Weekly Update - 11–31 May 2026"
date: 2026-05-31
description: "agentwerk ships v0.1.12 and v0.1.13 with a ticket system and tool compaction; plus a WordPress server rescued from OOM."
---

Been a busy stretch. Catching up on three weeks.

Most of the visible progress has been in [agentwerk](https://github.com/canvascomputing/agentwerk), the Rust crate for building agentic applications. It shipped **v0.1.12** and **v0.1.13** in quick succession around May 20–22. The big theme was rethinking how agents handle state: there's now a proper ticket system where agent messages get stored as ticket comments and the whole conversation is persisted to files. That's a meaningful shift from keeping everything in memory — it opens the door to long-running agents that survive restarts and can hand off work between sessions.

The other notable piece was **tool response compaction**: when an agent's context fills up with large tool outputs, it can now offload those to the ticket system rather than bloating the message history. There were also tidy API cleanups — renaming "steps" to "turns" (standard LLM terminology), unifying the export structure, and adding Claude hooks support so the framework integrates naturally with the Claude Code CLI.

On the ops side, I spent some time rescuing a WordPress site from an OOM-induced hang. The culprit was the classic Apache prefork + mod_php combo on a 1 GB instance with no swap — it eventually ran out of memory and froze. Fixed it by adding a 2 GB swapfile, switching to the event MPM with PHP-FPM, and capping MariaDB's `innodb_buffer_pool_size` at 128 MB. Nothing groundbreaking, but a good reminder that PHP-FPM really should be the default for anything running on a small server.
