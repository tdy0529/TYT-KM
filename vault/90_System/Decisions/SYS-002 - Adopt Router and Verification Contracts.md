---
id: SYS-002
type: system-decision
status: accepted
created: 2026-09-05
updated: 2026-09-05
aliases:
  - 路由與驗證契約決策
affects:
  - "[[AGENTS]]"
  - "[[90_System/Architecture]]"
  - "[[90_System/Workflows]]"
  - "[[90_System/Router Contract]]"
  - "[[90_System/Execution and Verification Contract]]"
---

# SYS-002 — Adopt Router and Verification Contracts

## Context

現有 Workflows 已定義八個大流程的 Trigger、Read、Decide、Write、Verify 與 Approval，但「常見後續」可能被誤解成預設流水線；跨流程任務也缺少統一的重路由、停止、未知路由與可稽查執行契約。只看最終內容或由執行模型自行宣稱完成，無法可靠確認走過的流程、檔案位置與必要同步是否正確。

## Decision

採用兩份低 context 的契約：

- [[90_System/Router Contract]] 只管理任務拆解、目前 workflow、候選 transition、重路由與停止。
- [[90_System/Execution and Verification Contract]] 定義日常運作的可觀察驗證；「最小」只是動作與 context 原則，不是對外模式名稱。

正式的一致性驗證資料另屬開發者環境，不進入日常載入路徑，也不隨使用者版發行；使用者練習日後由成熟結論另行轉譯。

各 workflow 的內部規則仍只由 [[90_System/Workflows]] 定義；生命週期區域與內容邊界由 [[90_System/Architecture]] 定義；type、欄位、狀態與正文契約由 [[90_System/Metadata Schema]] 定義。Contract 不重複這些細節。

使用者於 2026-09-05 審查 diff 後明確接受本決策。這項接受不擴大既有寫入權限；高影響語意決策仍依原核准規則處理。

## Rationale

- 把跨 block 控制與 block 內規則分離，避免 Workflows 持續膨脹。
- 日常運作不產生額外驗證紀錄；內部驗證資料與使用者運作規則分離。
- 先定義可人工執行的契約，後續 graph runner 可直接實作同一狀態模型。
- 以 filesystem diff 和確定性檢查補足模型自評的不足。

## Alternatives

### 把全部規則加入 Workflows

未採用。會增加每次任務的 context，並把路由、執行與領域流程混成一份大型文件。

### 立即實作 graph runner

延後。核心 transition 與判準尚未經真實案例驗證，過早寫 code 會固化錯誤假設。

### 只保留模型自我檢查

未採用。無法獨立確認模型是否漏讀、寫錯位置、漏同步或在修復後掩蓋第一次偏差。

## Consequences

- 收益：路由與停止條件可檢查；日常運作維持精簡；驗證方式可重現並能轉成程式。
- 成本：核心系統多兩份短文件；有寫入時需明確驗證實際 diff。
- 新風險：Contract 與 Workflows 可能漂移，因此每項規則只能有一個權威來源並以連結引用。

## Migration

- 新增兩份 Contract，接受後狀態為 reviewed。
- 在 AGENTS 加入最短載入入口。
- 在 Workflows 以八 block 導航索引取代 Prompt Router，並把跨 block transition／停止交由 Router Contract。
- 在 Architecture 加入執行控制迴圈與權威分工。
- Workflows 與 Architecture 在審查期間暫為 `active`，接受後恢復為 `reviewed`。
- 本決策接受後已在開發者環境建立獨立的一致性驗證層與發行邊界檢查。使用者版不得包含內部驗證資料、標準答案、執行紀錄或其導航連結。

## Rollback

- 移除兩份 Contract 與 AGENTS、Workflows、Architecture 中的引用。
- 還原 Workflows 的原始 Router 表頭與 Register／Ingest 轉移敘述。
- 以本次 Git diff 逐檔回復，不影響 Sources、Knowledge 或 Projects。

## Revisit when

- 實際使用顯示現有 transition 無法涵蓋真實任務。
- 日常任務因 Contract 產生不必要讀取或寫入。
- 同一類偏差反覆出現，值得由確定性 validator 或 graph runner 接管。
