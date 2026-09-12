---
id: SYS-007
type: system-decision
status: accepted
created: 2026-09-11
updated: 2026-09-11
aliases:
  - 寫作指南權威與專案關聯分工
affects:
  - "[[90_System/Metadata Schema]]"
  - "[[90_System/References/Authoring and Structure Guidance]]"
  - "[[90_System/Templates/Knowledge Note Template]]"
---

# SYS-007 — Clarify Authoring Authority and Project Relations

## Context

[[90_System/Decisions/SYS-006 - Unify Knowledge Writes and Modularize Core Rules]] 將寫作方法移到按需 Reference；指南仍有規範式語句，canonical 位置的具體分工與 project_refs／Relations 用途需要在正式契約中明確定義。

## Decision

使用者於 2026-09-11 明確同意評估建議並要求修改與 commit，本決策據此記為 accepted。

- Metadata 定義必要的 canonical 位置與專案關聯分工；建立或更新筆記時讀對應 type 的欄位與正文契約。
- Authoring and Structure Guidance 保持 active、按需載入，提供建議與例子；正式規則以 Metadata 與命中的 Workflow Spec 為準。
- project_refs 連 Project Context；Relations 解釋來源、應用或驗證情境，精確 provenance 另連 Worklog／Decision／Output。模板引用該契約。
- 保留目前 KN 準入規則與 method 定義，不恢復「操作步驟一律排除」等舊版清單。

## Rationale

讓必要約束位於受保護且寫入時會讀取的契約，並使機器可查詢的專案連結與人可讀的關係說明各有用途。

## Alternatives

- 將整份指南升為 reviewed 並列入 AGENTS：未採用，會把寫作建議納入核心治理，也不能單靠狀態解決載入問題。
- 原文補回 KN 排除清單：未採用，單篇摘要與專案特例的排除仍在，全面排除操作步驟會與可重用 method 衝突。

## Consequences

核心規格小幅增加；不新增欄位、type、workflow 或日常必讀的整份指南。專案關聯的具體落點更一致。

## Migration

更新 Metadata、指南與 KN 模板；既有內容不批次改寫，下次實質更新相關 KN 時核對專案關聯。Schema 變更後執行完整 lint 並記入當月日誌。

## Rollback

以本次獨立 commit 的反向變更回復；修改前 HEAD 為 `2c13cf0`。不回退其他工作區內容；日誌以追加 correction 保留歷史。

## Revisit when

- 指南出現核心契約未涵蓋的必要約束。
- project_refs 與 Relations 的分工持續造成重複或 provenance 遺漏。
