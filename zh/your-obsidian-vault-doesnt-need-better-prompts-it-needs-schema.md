---
layout: post
title: 你的 Obsidian Vault 不需要更好的 Prompt，它需要 Schema
lang: zh
date: 2026-03-14
permalink: /zh/your-obsidian-vault-doesnt-need-better-prompts-it-needs-schema
---

你用 Obsidian 搭配 Claude Code 的方式一直搞錯了。Claude 一直產生亂七八糟的 properties。Graph 一團糟。你塞更多指令進去。它還是搞錯。

這是資料建模的問題，不是 prompt engineering 的問題。沒有任何指令能修好一個毫無結構的 vault。你需要 schema。

### Templates 就是你的 Schema

Templates 是 Obsidian 對 agents 真正有用的地方。

Templates 預先定義每一個新筆記的 YAML frontmatter：固定的 properties、固定的值類型。Claude 不再亂猜 properties，因為 schema 已經存在了。

你會建立的每一個筆記，都是這兩種東西其中之一：

**Entities** - 會持續存在、不太改變的事物。公司、人物、專案。

**Events** - 會發生的事情。一場會議、一篇研究、一個想法。有時間戳記，連結到相關的 entities。

我總共用 6 個 templates。三種 entity 類型，三種 event 類型。如果某個東西不符合這些分類，我大概本來就不需要它。

### 一句話就能建立整個 Graph

Wiki-links 比 Notion 的 table-to-table 關聯更靈活。但你的 agent 不知道要把什麼連到什麼。

解法：每個檔案的 body 第一行放一句話的摘要，用 wiki-link 格式點名相關 entities：

> Overview of the \[\[XX deal\]\], from discussion with \[\[Bob\]\] at \[\[YY Conference\]\].

這一句話涵蓋了筆記最重要的所有 wiki-links，自動建立你的 graph。不需要手動建立連結，不會有斷掉的連接。

### 設定只要 5 分鐘

**一次性設定：** 定義你的基礎 templates。你的 vault 裡可能存在哪 5-8 種東西？不是 20 種。不是「之後再加」。限制本身就是重點。名稱要夠直觀，讓 Claude 能從情境判斷該用哪一個。

然後在你的 CLAUDE.md 裡加一行：「建立筆記之後，在 body 開頭加一句話的摘要，用 wiki-link 格式點名所有關鍵 entities。」這一條指令就讓每個新檔案自動變成 graph 的節點。結構自動化，判斷還是你的。

**每個新筆記：** Claude 照這個流程走：

```bash
obsidian templates                                    # see your templates
obsidian create name="My Note" template="Note"        # create with schema
obsidian prepend file="My Note" content="..."         # prepend the summary
```

摘要放在 body 裡，wiki-links 在這裡才真正有效；放在 frontmatter 裡是死文字。Properties 透過 CLI 來填，不是讓 Claude 猜 YAML 要怎麼寫。

現在打開你的 terminal，跑一下 `obsidian templates`。如果看到超過 10 個，開始刪。
