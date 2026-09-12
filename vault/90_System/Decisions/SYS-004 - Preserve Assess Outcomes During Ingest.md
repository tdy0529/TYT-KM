---
id: SYS-004
type: system-decision
status: accepted
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Assess 入庫交接決策
affects:
  - "[[90_System/Workflows]]"
---

# SYS-004 — Preserve Assess Outcomes During Ingest

## Context

SYS-003 已釐清未登記材料的後續追問仍屬 Assess，但現有規則只要求 Ingest 記錄來源主張、推論與 read scope，沒有明文要求在稍後 Register／Ingest 時回收先前多輪 Assess 形成的有效成果。Query／Persist 對已存在 Source Note 的後續補充有明確寫入路徑，Register 前的理解過程卻可能在對話結束後遺失。

使用者於 2026-09-10 明確接受以授權範圍控制 Assess handoff：未授權時只提出落點，只保存來源時回收 Source Note 成果，同時保存來源與知識時依序執行 Register／Ingest 與 Integrate。

## Decision

當同一份未登記材料經過多輪 Assess，且出現保存要求、保存方式詢問或已成立的 Register／Ingest Trigger 時，在目前工作鏈建立暫時的 Assess handoff inventory。inventory 只壓縮保存候選，不保存逐字對話，並把內容分類為 source claim、source-specific inference、reusable synthesis、user judgment、open question 或 discard。

依既有授權採三種處理：

1. 未授權保存時，只回報分類與建議落點，不寫入。
2. 只授權保存來源時，Register／Ingest 回收 Source Note 應承載的項目；完成 Verify 後只列出 Integrate 候選。
3. 授權保存來源與可重用知識時，先完成 Register／Ingest 與 Verify，再重新路由 Integrate；範圍清楚時不逐項重複詢問。

任何 user judgment 都要保持角色標示，不得轉成來源主張。若先前 Assess 脈絡已不可取得，必須揭露 handoff 不完整。高影響語意、reviewed 核心結論與其他既有核准條件不因本決策而放寬。

## Rationale

- 防止已判定有長期價值的理解只存在於聊天視窗。
- 保存壓縮後成果而非逐字對話，維持現有 context hygiene。
- 讓來源主張、來源特定推論、通用綜合與使用者判斷各自進入正確生命週期位置。
- 以使用者一次給定的清楚授權涵蓋連續 block，減少沒有實質決策價值的重複確認。

## Alternatives

### 保存完整 Assess 對話

未採用。會引入大量重複、已推翻想法與無權威區分的內容，也違反原始對話預設不保存的原則。

### Register 時只重新讀原件

未採用。雖能重建來源摘要，卻可能遺失使用者問題所揭露的假設、限制、比較與未解問題。

### 每個 handoff 項目都再次詢問

未採用。當使用者已清楚授權保存範圍時，逐項確認不會改變結果，只增加操作摩擦；高影響例外仍保留原核准門檻。

## Consequences

- Register／Ingest 前多一個暫時分類步驟，但不新增永久 handoff 檔案。
- Source Note 保存來源特定成果；可重用綜合經 Integrate 進入 Knowledge Note／Map；Project 或 Decision 保存情境性判斷。
- 完成驗證必須確認應保存項目已有落點或已明確列為未保存，不能只因建立 Source Note 就宣稱交接完成。
- 跨工作階段而無法取得先前對話時，系統只能依可用輸出與原件重建，並須揭露缺口。

## Migration

- 在 Assess 增加 handoff inventory、三種授權範圍與交接 Verify。
- 在 Ingest 增加 handoff 讀取、角色保留與「不得只留在聊天」Verify。
- 在 Integrate 增加 reusable synthesis 的接收與 Verify。
- 不回溯修改既有 Source Notes、Knowledge Notes、Projects 或歷史對話。

## Rollback

- 移除 Assess handoff 段與對應 Verify。
- 移除 Ingest 對 inventory 的讀取與交接 Verify。
- 移除 Integrate 對 reusable synthesis 的讀取與交接 Verify。
- 既有來源、知識與專案內容不受影響。

## Revisit when

- handoff inventory 經常過長，造成 Ingest 重複處理。
- 多來源 Assess 需要跨來源、跨工作階段的持久 staging type。
- 使用者需要保留部分逐字對話作為正式來源。
- 無法穩定判斷 source-specific inference 與 reusable synthesis 的邊界。
