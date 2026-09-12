---
id: SYS-REF-LLM-WIKI
type: system-doc
status: reviewed
created: 2026-09-03
updated: 2026-09-11
aliases:
  - LLM Wiki
---

# Karpathy — LLM Wiki

本頁記錄初始設計依據，採用脈絡見 [[90_System/Decisions/SYS-001 - Initial Architecture]]；現行操作以 [[90_System/Architecture]]、[[90_System/Router Contract]] 與 [[90_System/Workflows]] 所連的 Workflow Specs 為準。

原文：[LLM Wiki — A pattern for building personal knowledge bases using LLMs](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f#file-llm-wiki-md)

## 核心命題

一般 RAG 在每次查詢時重新從原始片段拼答案，沒有累積。LLM Wiki 則讓 LLM 在 raw sources 與使用者之間，持續建立一個結構化、互相連結、可更新的 Markdown Wiki。來源只處理一次，其理解、矛盾與交叉引用會成為持久資產。

## 三層

1. Raw sources：人選擇的原始材料，不由 LLM 改寫。
2. Wiki：LLM 建立、更新、交叉引用與保持一致的派生頁面。
3. Schema：規定結構、慣例與操作流程，並由人與 LLM 共同演進。

本 Vault 對應：

- Raw sources → 10_Sources
- Wiki → 20_Knowledge
- Schema → AGENTS.md 與 90_System
- 另外加入 Inbox 與 Projects 來管理未判定材料與情境工作

## 三個主要操作

### Ingest

不只建立單一摘要。新來源會產生 Source Note，並按其影響更新既有 entity、concept、comparison、Map、Index 與 log。一個來源可觸及多頁。

### Query

先讀 Wiki，再按需回到來源。好的比較、分析與新連結可回寫 Wiki，避免只存在聊天。

### Lint

定期檢查矛盾、過時主張、孤兒、缺頁、缺少交叉引用與資料缺口，並提出下一步問題或來源。

## Index 與 Log

- Index 是內容導向目錄，提供頁面連結與一行摘要，支援 LLM 先縮小範圍。
- Log 是時間導向、append-only 的操作歷史，使用一致標題以便搜尋與解析。

本系統用 Knowledge Index 實作前者；用按月 Logs 與固定條目格式實作後者。

## 人機分工

- 人：來源策展、探索、提問、判斷意義與審閱。
- LLM：摘要、交叉引用、整理、更新與簿記。
- Obsidian：人在一旁即時瀏覽、沿連結校訂、查看 graph 的 IDE。

## 對本系統的約束

- 不能只把來源放進資料夾而不整合。
- 不能把 Source Note 當成完成的 Wiki。
- 不能讓 Query 的高價值結果只消失在聊天。
- 不能忽略 Index、Log 與 Lint。
- 所有工具都是模組化的；規模與真實痛點出現前不增加基礎設施。
