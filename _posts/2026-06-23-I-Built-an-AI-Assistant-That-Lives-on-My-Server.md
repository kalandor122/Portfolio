---
title: "I Built an AI Assistant That Lives on My Server"
description: >-
  How I set up a self-hosted AI agent with Hermes. Custom MCPs bridging
  it to my personal Life OS tools, Home Assistant integration, persistent
  memory, and Telegram chat. Full control, no subscriptions.
date: 2026-06-23
author: "Füvesi Magor"
tags: [ai, agent, hermes, self-hosted, mcp, home-assistant, homelab]
---

I have been running a homelab for a while. Self-hosted services, Docker containers, a Coolify instance to manage it all. The next step was obvious: if I can self-host my own cloud, I can self-host my own AI.

AI assistants are everywhere these days. ChatGPT, Claude, Gemini. They all run on someone else's server. I wanted something that lives on my hardware, connects to my tools, and actually knows my context. So I built one.

## Meet Hermes

[Hermes Agent](https://hermes-agent.nousresearch.com) is an open source AI agent framework by Nous Research. You configure it once. Pick your model, connect your platforms, wire up your tools. Then it runs on your own machine. Mine sits on a Linux server with DeepSeek V4 Flash and talks to me through Telegram.

The base setup is simple:

* **Hermes Agent** runs as a persistent service.
* **Telegram** is the frontend. I DM it like a person.
* **Mnemosyne** is the memory system. It remembers who I am and what I am working on across sessions.
* **Skills** are packaged workflows it can load on demand.

The really useful parts are the things I plugged into it.

## Skills

Hermes has a skill system. Packaged workflows it can load on demand. I have curated a collection that covers most of what I need day to day.

**Document conversion.** I installed [Microsoft MarkItDown](https://github.com/microsoft/markitdown) so Hermes can take any file I throw at it. PDF, DOCX, XLSX, even images with OCR. It turns them into clean Markdown instead of garbled binary. The skill is called `markitdown-convert-before-read` and kicks in automatically when I send a file.

**Humanizer.** Makes the agent's writing sound less like an LLM and more like a person. I swapped the old version for the [Blader Humanizer](https://github.com/blader/humanizer) skill. It picks the right tone without me having to prompt.

**Code review, debugging, testing.** Systematic workflows that enforce quality gates before I push anything.

**Jekyll blog management.** Hermes knows how to write, format, and commit posts to this very site.

**PC shutdown.** A skill that safely powers down my PC through Home Assistant. Uses the soft shutdown button instead of cutting the plug.

**Google Workspace, Spotify, YouTube transcripts.** Hermes can read my emails, queue music, or summarize a video. All through skills.

The nice thing is that I can add a new capability without writing code. I just describe the workflow and the agent learns it.

## Custom MCP Servers

MCP, or Model Context Protocol, is how you give an AI agent access to your own tools. I built three MCP servers that bridge my personal infrastructure into the agent.

### Life OS MCP

Life OS is my personal tool suite. A todo app, a habit tracker, and a projects manager that I built for myself and use every day. I open sourced it on GitHub, but it is really designed around my own workflow. I wrapped the whole thing in an MCP server so Hermes can interact with it directly.

I can list my projects and tasks, create new ones by asking, check my daily todos, log work hours. Instead of opening a web app I type "What is on my todo list today?" and Hermes queries the Life OS API directly.

### Wishlist MCP

I built a [wishlist manager](https://github.com/fuvesi). FastAPI backend, React frontend, PostgreSQL. Then I added an MCP server on top. I can say "Add this AliExpress link to my wishlist" or "Run the haul builder with a 100 dollar budget." Hermes handles the CRUD operations and runs a knapsack optimization to tell me the best items to buy.

### Coolify MCP

My whole homelab runs on Coolify. Through its MCP integration, Hermes can check deployment status, view logs, restart containers, and manage environment variables from chat. No SSH, no dashboard, just a message.

## Smart Home

My Home Assistant instance is connected too. I can ask Hermes to turn off the living room lights, check sensor readings, or query any device. The message goes from Telegram to Hermes to the Home Assistant API and back.

It sounds simple. The seamless feel is what makes it a real assistant instead of a bunch of scripts.

## Memory

The Mnemosyne memory system is one of my favourite features. Hermes keeps context across sessions. My preferences, project details, environment quirks. When I pick up a conversation from yesterday it is not starting from scratch. It knows what Life OS is, what apps I run on Coolify, how to navigate my infrastructure.

I can also save durable facts that persist forever. Setup details, recurring corrections, personal preferences. The longer I use it, the better it gets.

## Scheduled Jobs

Cron jobs in Hermes run on a schedule, not just when I chat. I have morning briefings that check my todo list and report back. Periodic code audits on my repositories. Reminders for recurring tasks.

Each job runs with full context. It loads the right skills and delivers results back to my Telegram.

## Why This Matters

Running your own AI agent is not only about privacy, though that is a nice bonus. A generic chatbot can write poems or explain quantum physics. It cannot query your database, turn off your lights, or audit your codebase. A self-hosted agent with custom MCPs can, because that integration is exactly what you built.

Building those MCP servers was the most rewarding part. You extend the AI instead of just consuming it, shaping it to fit your actual workflow. Every new tool I self-host becomes a potential new capability for Hermes.

It is not perfect. The agent still hallucinates occasionally, and the memory system can get noisy if I do not prune it. But it keeps getting better the more I use it, and I would rather have an assistant I control than one I rent.

---

*Stack: Hermes Agent · DeepSeek V4 Flash · OpenCode Go · Python · FastAPI · React · PostgreSQL · Home Assistant · Coolify · MCP · Mnemosyne · Skills · MarkItDown · Telegram*
