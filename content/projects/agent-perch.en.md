+++
title = 'agent-perch: Keeping Long-Running AI Agents Alive'
date = '2026-10-13'
draft = false
description = 'A single-file, stdlib-only supervisor that keeps a fleet of agent processes (e.g. Claude Code bots) running on one machine.'
tags = ['AI Agents', 'Reliability', 'Python', 'tmux']
+++

**The problem:** running several always-on agents on a Raspberry Pi, three things kept failing: a session died silently, a session froze on a keypress prompt nobody could answer, and agents needed to talk to each other.

**What I built:** the generic version of the watchdog I wrote for my own fleet:
- tmux is the process boundary; a dead session is restarted. "Frozen" means an unchanged screen *and* a known marker, since either signal alone misfires.
- Known dialogs are answered with configured keys, so a restart does not just show the same prompt again.
- A file-based mailbox (jsonl) lets agents message each other, instead of typing into another agent's terminal.
- A crash-loop halt (3 restarts in 10 minutes) stops and alerts once; a small dashboard and alert hook round it out.

**Trade-offs are written down:** each design decision in the README states its cost (for example, "alive" means the session exists, not that work is progressing). It is single machine and single tenant, with no auth or isolation, and says so.

Stack: Python 3.11+ (standard library only), tmux, MIT license.

**Links:** [GitHub repo](https://github.com/tses89214/agent-perch)
