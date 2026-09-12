---
id: SYS-DOC-EXECUTION-VERIFICATION-CONTRACT
type: system-doc
status: reviewed
created: 2026-09-05
updated: 2026-09-10
aliases:
  - 執行與驗證契約
  - Verification Contract
---

# Execution and Verification Contract

## 目的與適用範圍

驗證依靠可觀察證據，不以執行模型自己的完成聲明為準。本契約只規範使用者日常運作中的執行與驗證；「最小」是控制動作與 context 的設計原則，不是另一種使用模式。

純讀取或一次性回答不建立驗證檔。有寫入時確認預計位置、實際變更、workflow Verify、局部 lint 與需人確認處。

## 權威分工

- [[90_System/Router Contract]]：決定何時執行、重路由或停止。
- [[90_System/Architecture]]：定義生命週期區域與內容邊界。
- [[90_System/Workflows]]：提供 workflow 索引與共同契約；命中的 Workflow Spec 定義具體 Write／Handoff 與完成條件。
- [[90_System/Metadata Schema]]：定義 type、欄位、狀態與正文要求。
- 本文件：定義日常寫入如何留下足以檢查的證據並對照預期。

發生衝突時，先停止高影響寫入並回到上述唯一權威文件，不在完成回報中臨時發明規則。

## 日常運作

有寫入時依序執行：

1. 寫入前說明目前 workflow、預計產物與位置，並搜尋同義詞、既有頁面與可能衝突。
2. 只做目前 workflow 所需的最小變更；原始來源、高影響語意與需核准範圍遵守既有權限。
3. 直接檢查實際新增、更新、移動與刪除，並把結果和預計位置對照；不得只依賴文字回報。
4. 逐項執行目前 workflow 的 Verify，再對變更檔與一階鄰接頁執行局部 lint；若核心 Workflow、Schema 或大型結構變更，依 [[90_System/Workflow Specs/Lint and Refactor]] 執行完整 lint。
5. 回報 created、updated、removed、未解問題、修復與待確認事項；若計畫與實際不同，明列偏差及原因。
6. 依 [[90_System/Router Contract]] 的路由輸出，回報本次規格未涵蓋而自行決定之處，以及已成立但未執行的 workflow Trigger。驗證過程中做出的語意判斷（例如判定某個 lint 命中為非問題）屬於前者；純工具失敗與重試不必記錄。

若正確結果是不寫入，停止即可，不建立空白紀錄。

## 日常核對面向

每次寫入至少核對：

- 流程路徑：目前 workflow 是否有可觀察的 Trigger 事實支持；跨 block 前是否完成目前 Verify 並重新路由；是否執行了沒有成立理由的 block。
- 檔案落點：內容是否落在正確生命週期區域，檔名與 ID 是否符合角色。
- 結構：frontmatter、必要段落，以及該 type 適用時的 locator、read scope 與狀態是否符合契約。
- 同步：應更新的 Index、Map、Context、Decision 或 Log 是否確實更新。
- 邊界：來源原件與禁止範圍是否保持不變，是否產生重複頁或非必要檔案。
- 語意：來源主張、LLM 推論、使用者判斷與決策是否分開；證據、假設、未知與限制是否明示。
- 申報：規格未涵蓋而自行決定之處、以及已成立但未執行的 Trigger，是否已在完成回報中列出；沉默地做選擇視為未通過。

內容正確但位置、狀態或必要同步錯誤，仍未通過 Verify。日常運作以實際產物、diff、lint 結果與完成回報供人檢閱，不另製造逐步紀錄。

## 日誌

日誌位於 `90_System/Logs`，按月 append-only，標題固定為 `## [YYYY-MM-DD] workflow | 簡短標題`。每筆至少包含 Scope、Created、Updated、Result、Review。

記錄 ingest、integrate、完整 lint、實際修正問題的局部 lint、refactor、schema／workflow／system change，以及 Project 的建立、里程碑、暫停與結束。Query／Persist 沒有 substantive write，不另記 persisted query；Project-origin 知識寫入統一記為 integrate。單純讀取、無持久變更的問答、微小排版與 Project 日常工作階段不記系統日誌。

歷史條目不改寫；錯誤以新的 correction 條目修正。

## 偏差與修復

發現計畫外變更、錯誤位置或必要同步缺漏時，先停止後續 substantive write，回報偏差，再處理可機械判斷的修復；不得用修復後結果掩蓋已發生的偏差。

可自動修復無語意歧義的機械問題，例如明確的格式、失效連結、必要欄位、索引或日誌漏更新。科學結論、來源適用性、accepted decision、reviewed 核心結論與核心規則只提出差異或方案，等待使用者決定。
