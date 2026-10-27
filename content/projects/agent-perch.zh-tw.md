+++
title = 'agent-perch：讓長時間運行的 AI agent 不掛'
date = '2026-10-13'
draft = false
description = '單一檔案、只用標準函式庫的 supervisor，讓一台機器上的 Claude Code 等 agent 持續運作。'
tags = ['AI Agents', 'Reliability', 'Python', 'tmux']
+++

**問題：** 在 Raspberry Pi 上同時跑多個常駐 agent 時，反覆遇到三件事：session 默默死掉、卡在沒人能回答的按鍵提示、agent 之間需要互相傳訊息。

**做法：** 把原本寫給自己用的 watchdog 抽成通用版本：
- 以 tmux 作為行程邊界，session 掛掉就重啟；畫面不變且出現已知提示文字才判定為卡住。
- 已知的對話框用設定好的按鍵自動回應，避免重啟後又看到同一個提示。
- 以檔案信箱（jsonl）讓 agent 互傳訊息，不直接對別人的終端機打字。
- 3 次重啟 / 10 分鐘就停止並通知，避免無限重啟迴圈；提供儀表板與告警指令。

**取捨寫在 README：** 每個設計決策都記錄了代價（例如存活的定義是「session 存在」，不代表工作有進展）。目前是單機、單一使用者，沒有認證與隔離，這是刻意標示的限制。

技術：Python 3.11+（僅標準函式庫）、tmux、MIT 授權。

**連結：** [GitHub 專案](https://github.com/tses89214/agent-perch)
