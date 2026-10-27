+++
title = 'Stark Support Bot：LLM 客服機器人的防護與評測'
date = '2026-10-27'
draft = false
description = '用「從最差基準開始、一次只加一層防護」的方法，量測 LLM 客服機器人擋下 prompt injection 的能力。'
tags = ['LLM', 'RAG', 'Evaluation', 'Guardrails']
+++

**要回答的問題：** 每加一層防護，到底多擋下幾個攻擊？不是憑感覺，而是用固定的測資量出來。

**做法：** 以虛構的飛船產品文件做 RAG 客服機器人，從完全不設防的版本（L0）開始，每次只加一層防護，並用同一組 28 個攻擊與 6 個正常問題重跑。

| 等級 | 新增的防護 | 擋下的攻擊（95% 區間） | 正常問題答對 |
|---|---|---|---|
| L0 | 無（文件全塞進 prompt） | 16 / 28（44–69%） | 6 / 6 |
| L1 | 回答規則（只依文件回答） | 22 / 28（66–87%） | 6 / 6 |
| L2 | 輸入隔離＋不信任輸入規則 | 24.5 / 28（76–94%） | 6 / 6 |
| L3 | 輸入分類器與路由 | 28 / 28（94–100%） | 6 / 6 |

（每個等級跑 2 次取平均，使用單一免費模型。）

**評測方法的重點**
- 不用 LLM 當裁判：以 canary 字串與文件事實做確定性判定，免費、可重現，但判定較粗糙。
- 小樣本一律附信賴區間；差一兩個攻擊視為雜訊，不排名單一步驟的貢獻。
- 143 筆分類器測資（57 筆手寫、86 筆 LLM 草擬後人工審核），正確 137 筆。
- 模型失敗不算成功擋下：分類器失效時轉人工並註明原因，且不計入分數。

**限制：** 測資小、只用一個免費模型、資料是虛構的，結果不能直接推論到其他模型或真實客服流量。

技術：Python、FastAPI、bge-m3 向量檢索、OpenRouter、MLflow。

**連結**
- [GitHub 專案](https://github.com/tses89214/stark-support-bot)
- [完整報告（中文）](https://tses89214.github.io/stark-support-bot/results/report.html)・[Full report (English)](https://tses89214.github.io/stark-support-bot/results/report.en.html)
