---
id: SYS-WF-LINT-REFACTOR
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Lint Workflow
  - Refactor Workflow
---

# Lint／Refactor

## 邊界

- Lint 檢查、列出問題，並只修正無語意風險的機械錯誤。
- Refactor 改變頁面邊界、名稱、連結結構、Schema 或核心結論。

## 局部 lint

每次寫入後檢查變更檔與一階鄰接頁：

- frontmatter、必要欄位、enum、日期、ID 與檔名。
- 數學分隔符；程式碼區塊外不得殘留 `\(`、`\)`、`\[`、`\]`。
- 新 Wikilink 是否解析，外部主張是否有來源與 locator。
- Index、Map、Context 或 Decision 是否需要同步。
- 同名、明顯重複頁，以及 workflow 未要求或未授權的頁面。

通過不建立報告；實際修正或發現風險才依執行契約記錄。

## 完整 lint Trigger

- 使用者明確要求。
- 每累積 10 個 processed Source Notes。
- Project 里程碑、暫停或結束。
- Schema、Workflow 或大型結構變更。
- 出現失效連結、重複筆記、索引落後、無來源主張、長期 contested、角色混雜、孤兒或找不到已知內容等漂移訊號。

門檻是預設啟發式，不為湊數執行無價值掃描。

## 完整 lint 檢查

- 結構：孤兒與失效連結、重複 ID／名稱／別名／概念、Index／Maps／Base 差異、頁面角色與大小。
- 證據：外部主張缺來源或 locator、Source Note 與原件不一致、跨頁數值漂移、Project 複製來源 claim、partial 被當成完整閱讀。
- 語意：未標示衝突、supersede 漂移、術語定義漂移、推論／觀察／決策／來源主張混淆、缺少應獨立成頁的概念。
- 時效：last_verified 過舊、needs-review 或 contested 無下一步。
- 導航：高價值頁無 Map、Map 無路徑說明、不合理孤兒、跨領域連結缺失或過度。

## Lint 輸出

依 error、warning、suggestion 列出檔案、問題、證據、建議修復與核准需求。完整 lint 一律記錄於當月日誌。

## Refactor

可直接做：格式統一、明確失效連結、缺少索引條目、無歧義 metadata。

需先確認：合併、拆分、刪除、批次改名、大量搬移、Schema／狀態變更、reviewed 核心結論變更。

完成後重跑相關 lint，並記錄 changed、reason、migration 與 rollback。

## Verify

- 所有 finding 都有嚴重度與證據；未把語意判斷偽裝成機械修復。
- 實際改動在核准範圍內，必要同步完成。
- Refactor 後相關 lint 通過；完整 lint 已寫入日誌。

## Approval

遵守上方 Refactor 邊界與 [[AGENTS]] 的寫入權限。
