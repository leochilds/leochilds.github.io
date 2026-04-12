---
title: Letting AI Run the Show
date: 2026-04-12
description: Why I handed this site over to AI agents and what that actually looks like in practice.
---

I've had a personal GitHub Pages site for years. It was always a bit of a chore -- the kind of project that sits there gathering dust because updating it never quite makes it to the top of the list. So when I decided to overhaul it, I figured it was the perfect low-risk place to throw caution to the wind and let AI handle most of the work.

## The rewrite

The entire site was rewritten from scratch using [Claude Code](https://claude.com/claude-code) with Claude Opus, replacing the old Jekyll setup with an [Astro](https://astro.build/) static site.

Claude used the GitHub CLI to pull in all my public repositories, check which ones have live GitHub Pages deployments, identify forks and their upstream repos, and organise everything into categories. The whole thing -- layouts, styling, dark mode, blog infrastructure, and GitHub Actions deployment -- was built in a single session.

## The automation

I have a weekly scheduled agent that runs every Sunday evening. It scans my repos and organisations for changes, updates the projects page if anything is new, and writes a short blog post summarising the week's activity. It follows the same PR workflow as everything else: branch, commit, create a PR, wait for reviews, address comments, merge.

Speaking of reviews -- [Gemini](https://cloud.google.com/gemini) is watching the repo and leaving PR review comments. It has already caught some genuine improvements, like adding `target="_blank"` and `aria-label` attributes to external links. It also suggested I shouldn't let AI merge without human approval, which I politely declined. This isn't a critical codebase.

## The line between automation and expression

I want to be clear about what AI is doing here and what it isn't. The weekly updates and project tracking are chores -- maintenance tasks that I historically never bothered doing. AI is good at chores. It's reliable, it doesn't get bored, and it doesn't procrastinate.

But there is no replacement for genuine human art and creativity. I'll be writing blog posts myself too, because writing is a form of expression, not just information transfer. The automated posts are functional. The human ones are mine. That distinction matters.

## The stack

For the curious, here's what's running:

- **Astro** for static site generation
- **Claude Code** (Opus) for the initial build and ongoing changes
- **GitHub Actions** for deployment on every merge to main
- **Gemini Code Assist** for automated PR reviews
- **Claude Code scheduled agents** for weekly site maintenance

The source is public at [github.com/leochilds/leochilds.github.io](https://github.com/leochilds/leochilds.github.io) if you want to see how the sausage is made.
