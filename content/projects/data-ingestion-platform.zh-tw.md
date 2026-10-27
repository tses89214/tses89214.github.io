+++
title = 'Data Ingestion Platform：讓沒有技術人員的部門也能貢獻資料'
date = '2025-03-11'
draft = false
description = '行銷、業務、營運部門上傳 CSV，平台以資料團隊維護的 schema 自動驗證。'
tags = ['Data Engineering', 'Data Quality', 'Docker']
+++

**問題：** 沒有技術人員的部門手上有資料，但沒有簡單又可靠的方式交給資料團隊，常見的結果是格式不一、欄位錯誤，要來回確認。

**做法：** 提供網頁介面，部門自己上傳 CSV；資料團隊維護每張表預期的 schema，上傳後平台驗證並顯示預覽，成功或失敗都會明確回報。支援不同表使用不同 schema，以 Docker Compose 一行指令啟動。

**限制（README 已誠實列出）：** 這是概念驗證。目前只驗證前十筆資料、支援的型別有限（str、int、float、datetime、date）、檔案存在本機、沒有帳號管理。下一步是全量驗證、雲端儲存與權限控管。

技術：Python、Docker Compose。

**連結：** [GitHub 專案](https://github.com/tses89214/Data-Ingestion-Platform)
