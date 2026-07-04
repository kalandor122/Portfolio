---
title: "I Made Minesweeper You Can Play Over SSH"
description: >-
  A Dockerized SSH server that runs Minesweeper in your terminal.
  Multiplayer, rate-limited auth, and container hardening.
  Built with Python and asyncssh.
date: 2026-07-04
author: "Füvesi Magor"
tags: [python, ssh, game, docker, self-hosted, homelab]
---

I have always liked those SSH sites. The ones where you SSH in and some interesting service greets you instead of a shell. There is one where you can order coffee from the terminal. Another where you play a text adventure. I wanted to build something like that.

I already had a terminal Minesweeper game sitting around from a previous project. So I turned it into an SSH server.

## How it works

You connect with any SSH client. No client software, no browser, just the `ssh` command that ships with every OS.

```
ssh minesweeper@mine.magor-lab.hu -p 2222
```

Enter the shared password and you are in a full Minesweeper game. Arrow keys to move, D to dig, F to flag, R to restart, Q to quit.

Three difficulty levels:

| Level  | Size   | Mines |
|--------|--------|-------|
| Easy   | 9x9    | 10    |
| Medium | 16x16  | 40    |
| Hard   | 16x30  | 99    |

Multiple people can play at the same time. Everyone gets their own game state.

## The stack

Python, asyncssh, and Docker. That is it.

The game logic is a clean 130 lines. The SSH server wraps it with asyncssh, which handles the protocol, terminal detection, and session management. The UI renders with ANSI escape codes and Unicode box drawing, so it works in any terminal that supports 256 colors.

The Dockerfile pins a specific Python slim image digest for reproducibility. The container runs as an unprivileged user with a read-only root filesystem, resource limits, and a tmpfs for temporary writes.

## Security decisions

Exposing an SSH server to the public requires some care. I made a few deliberate choices.

**No default password.** The server refuses to start if `MINE_PASSWORD` is unset or shorter than 12 characters. You generate it at deploy time.

**Rate limited auth.** Each IP gets 10 attempts per 5 minute window. After that the server stops responding to that address until the window resets. Prevents brute forcing without needing fail2ban.

**Concurrent connection cap.** 64 simultaneous players max. This avoids resource exhaustion on the host.

**Session timeouts.** Idle connections get dropped after 10 minutes. Absolute session limit at 60 minutes. Nobody sits on an open connection forever.

**Structured audit logging.** The server logs auth attempts, connections, and disconnections. Passwords are never logged.

**Host key generated at first start.** No baked-in credentials, no default host key in the image.

## Deployment

One compose file, one environment variable, one command.

```bash
MINE_PASSWORD=$(openssl rand -base64 24)
echo "MINE_PASSWORD=$MINE_PASSWORD" > .env
docker compose up --build -d
```

The password can be anything long enough. I picked something memorable for my instance since friends are the audience.

## Where to play

If you want to try it, connect here:

```
ssh minesweeper@mine.magor-lab.hu -p 2222
```

The password is `fuvesi.hu123`. Give it a shot.

The source is on GitHub at [github.com/kalandor122/ssh_minesweeper](https://github.com/kalandor122/ssh_minesweeper) if you want to host your own copy.

---

*Stack: Python · asyncssh · Docker · Minesweeper · SSH*
