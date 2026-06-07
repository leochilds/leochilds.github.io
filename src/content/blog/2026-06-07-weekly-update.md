---
title: "Weekly Update - 1–7 June 2026"
date: 2026-06-07
description: "Setting up a self-hosted AI agent platform on AWS with email and WhatsApp integrations, plus agentwerk's new interactive mode and context compaction work."
---

Most of this week was infrastructure — getting a self-hosted AI agent platform running on AWS. I've been meaning to do this properly for a while, and it finally came together.

The setup uses EC2 behind Tailscale (no public ports at all), Docker for the services, and Terraform to manage everything reproducibly. The interesting part is the agent configuration: there's a WhatsApp channel with an allowlist, and an email triage agent that reads from a Proton Mail Bridge over loopback IMAP. The email agent runs on a 30-minute heartbeat, has a sandboxed exec environment with only `himalaya` allowed, and works out of its own isolated workspace. Getting the Proton Bridge working inside Docker took some wrangling — it caches the full mailbox locally (so you need more disk than you'd expect), and the bridge uses a self-signed CA so the IMAP client needs to trust it explicitly on the loopback interface.

Meanwhile, [`agentwerk`](https://github.com/canvascomputing/agentwerk) had a productive sprint. The headline feature is **interactive mode** — agents can now pause mid-turn and wait for user input rather than immediately failing on an unexpected bare-text response. Alongside that, context window compaction got a significant overhaul: it now handles oversized user messages by chunking and summarising them, covers both Anthropic and OpenAI's different error dialects for context overflow, and logs compaction events with window usage stats so you can see what's happening. The transcript format changed too — comments were renamed to replies and split into an append-only `replies.jsonl` per ticket, which is a much cleaner structure for long-running agents.
