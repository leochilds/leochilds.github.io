---
title: "Weekly Update - 4–10 May 2026"
date: 2026-05-10
description: "The cryptography course site got a serious batch of OTP attack demos — crib dragging, WEP IV collisions, and the classic Netscape SSL crack."
---

Most of the energy this week went into the [Kyri-Cou cryptography site](https://kyri-cou.github.io/cryptography/). Three new interactive attack pages landed, all tied to the one-time pad vulnerabilities lesson.

The first is a **crib dragging** demo. You get two messages encrypted with the same keystream — like the classic Soviet key reuse mistake — and you drag a known word ("the", "and", whatever you like) across the XOR of the two ciphertexts. Every position scores how printable the result is, sorted best-first. It's one of those attacks that sounds abstract until you can actually do it with your hands, and I think the interactive version makes it click in a way a diagram doesn't.

The second page simulates the **WEP IV collision** — the birthday-paradox flaw that made WEP useless in practice. It runs a live RC4 simulation, counts packets until two IVs collide (usually a few thousand), then shows you what you learn from the collision. I had to fix the crib section after the initial version: the old implementation was XORing the LLC/SNAP header against itself and always getting zeros, which wasn't teaching anything useful. The fixed version uses the full known plaintext to actually recover packet B's payload.

Third is a **weak PRNG** page, recreating the 1994 Netscape SSL crack. The seed was `time ^ PID`, giving maybe 17 bits of effective entropy. The demo brute-forces it live in the browser — you watch the counter tick up, and it finds the seed in seconds. It's a bit humbling when you realise this was shipping in a commercial browser.

Elsewhere, [`LionPDF`](https://github.com/leochilds/LionPDF) and [`agentwerk`](https://github.com/canvascomputing/agentwerk) both picked up commits this week too. Nothing I can summarise neatly, but both are moving.
