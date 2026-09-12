---
id: SYS-001
type: system-decision
status: accepted
created: 2026-09-03
updated: 2026-09-03
aliases:
  - 初始系統架構決策
affects:
  - "[[90_System/Architecture]]"
  - "[[90_System/Workflows]]"
  - "[[90_System/Metadata Schema]]"
---

# SYS-001 — Initial Architecture

## Context

需要建立一個不綁定特定領域、可讓 LLM 與 Obsidian 長期協作的知識系統。原 Vault 只有操作練習與錯置設定；使用者允許清除原有內容。設計以 [[90_System/References/Karpathy - LLM Wiki|Andrej Karpathy 的 LLM Wiki]] 為最高原則，並參考 [[90_System/References/Knowledge Pipeline - Design Adaptation|knowledge-pipeline]] 對系統、知識、專案、Context、Decision 與 promotion 的分離方法。

## Decision

採用五個生命週期區：

- 00_Inbox：未判定輸入。
- 10_Sources：不可任意改寫的來源。
- 20_Knowledge：由 LLM 持續維護的 Wiki。
- 30_Projects：目標與情境限定的工作。
- 90_System：Schema、Workflow、Decision 與維護。

內容導航使用一個全域 Knowledge Index、多張語意 Maps、Obsidian Bases、Wikilinks 與 backlinks。日誌按月 append-only。專案成果以增量 Promote 進入 Knowledge。

## Rationale

- 保留 LLM Wiki 的 raw／wiki／schema 核心邊界。
- Inbox 降低收件摩擦。
- Projects 防止情境性工作污染通用知識。
- Maps 解決多領域與多視角，不需要複製筆記或建立龐大資料夾分類。
- Properties 與 Base 支援維護；Index 提供 LLM 低成本語意檢索。
- 按事件 lint 比固定每日維護更簡單且更符合實際風險。

## Alternatives

### 以主題建立頂層資料夾

未採用。跨領域內容會被迫複製或只能放在單一位置，重構成本高。

### 所有工作都直接寫入 Knowledge

未採用。專案假設、暫時結果與通用知識會混淆。

### 先建向量資料庫或完整自動化

未採用。初始規模沒有證據顯示需要，會增加維護面與黑箱行為。

### 只有一個 Index 與一個 Log

保留其功能，但調整實作：一個 Knowledge Index 作內容目錄；Maps 與 Base 分擔語意導航與狀態篩選；日誌按月分檔並保留一致標題格式。

## Consequences

- LLM 每次 ingest 或 integrate 必須維護多個受影響頁面、Index 與日誌。
- 使用者不需要先決定主題資料夾。
- 系統品質依賴 locator、狀態與 promotion 判斷，而非只依賴 Markdown 數量。
- 初期有少量手動或 LLM 維護成本，但避免日後從散落文件重建理解。

## Migration

初始建置直接建立新結構。舊的空資料夾與失效設定移除；保留 Obsidian 基礎設定與既有 Excalidraw 外掛。

## Rollback

所有 Markdown 與設定由 Git 基線保存。可從初始 commit 比較或復原個別檔案；原始來源仍應另有備份。

## Revisit when

- 搜尋已知內容的失敗率明顯上升。
- 正式頁面超過約 1,000 且 Index 無法有效縮小範圍。
- 多人共同寫入，需要角色與 review queue。
- 多媒體或資料集需要可重現的處理 pipeline。
