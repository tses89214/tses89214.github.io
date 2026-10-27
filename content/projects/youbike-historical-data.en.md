+++
title = 'YouBike Historical Data'
date = '2025-06-22'
draft = false
description = 'Public data only has live bike counts, so I built the history myself to answer "when does my station get restocked?"'
tags = ['Data Engineering', 'Open Data', 'Python']
+++

**The problem:** Taipei's public YouBike data only exposes live bike counts, so it cannot answer "when does the station near my home get restocked?" or "what hours is it usually empty?".

**What I built:** a history of my own:
- A job calls the public API every ten minutes and splits the response into two tables: `sites` (a station dimension table) and `slots` (a fact table of bike counts per station).
- Data lands in a personal database first; at 1 a.m. each day the previous day's `slots` are published to GitHub, and `sites` is published only when something changes.
- A documented schema plus the traps I found: total slots do not always equal rentable plus returnable, some stations go months without updates, and I chose the station's upload time over the system's receive time (the reasoning is in the README).
- Unit tests (pytest) and an alerting module.

The data is public in the repo's `data/` directory. The latest automatic update in the repo is from June 2025.

Stack: Python, pytest, GitHub as the publishing channel.

**Links:** [GitHub repo](https://github.com/tses89214/youbike-historical-data)
