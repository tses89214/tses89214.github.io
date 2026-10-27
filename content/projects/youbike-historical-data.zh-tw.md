+++
title = 'YouBike 歷史數據資料庫'
date = '2025-06-22'
draft = false
description = '公開資料只有即時車輛數，所以自己累積歷史資料，回答「這個站什麼時候會補車」。'
tags = ['Data Engineering', 'Open Data', 'Python']
+++

**問題：** 台北市 YouBike 的公開資料只有即時車輛數，無法回答「我家旁邊的站點何時會補車？」「幾點最常沒車？」。

**做法：** 自己累積歷史資料：
- 每十分鐘呼叫一次公開 API，拆成兩張表：`sites`（站點維度表）與 `slots`（各站車輛數事實表）。
- 資料先暫存在個人資料庫，每天凌晨一點把前一天的 `slots` 上傳到 GitHub；`sites` 只有在資料異動時才上傳。
- 有 schema 文件，並說明資料的陷阱：總格數不一定等於可借加可還；部分站點可能數個月沒有更新；時間欄位選用站點上傳時間而非系統接收時間，原因寫在 README。
- 程式有單元測試（pytest）與異常告警模組。

資料目前公開在 repo 的 `data/` 目錄，repo 最近一次自動更新是 2025 年 6 月。

技術：Python、pytest、GitHub 作為資料發布管道。

**連結：** [GitHub 專案](https://github.com/tses89214/youbike-historical-data)
