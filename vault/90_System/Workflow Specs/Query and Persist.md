---
id: SYS-WF-QUERY-PERSIST
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Query Workflow
  - Persist Gate
---

# Query／Persist

Query 回答；Persist 判斷問答新增成果是否值得保存、屬於哪個權威區域，以及是否已有授權。這個 block 不直接修改 Knowledge、Source Note 或 Project；需要保存時完成 Verify，再由 Router 重路由至唯一負責該區域的 workflow。

## Trigger

- 從庫內既有內容回答解釋、比較、分析、設計或決策問題。
- 材料已在 Knowledge Notes、Maps、Source Notes 或已登記原件。
- 問題雖由先前 Assess 引出，但暫時移除未登記材料後，Wiki 仍足以回答。

先前 Assess 不會把未登記材料變成持久證據。答案仍依賴庫外材料時走 Assess；Wiki 沒答案時說明缺口，不在 Query 裡直接引用外部新材料。

## Read

1. 先讀 [[20_Knowledge/Knowledge Index]]。
2. 讀命中的 Maps 與 Knowledge Notes。
3. 精確引用、時效驗證或衝突處理需要時，再讀 Source Notes 與原件。
4. Wiki 無答案時可檢索 30_Projects，但必須聲明 Wiki 缺口、標示專案狀態與證據成熟度，不把它併入通用結論。
5. 都沒有答案時停止 Query；需庫外材料則交回 Router 判斷 Assess。

下鑽長原件時依 [[AGENTS]] 回報實際抽取、核對與未核對範圍。

## Answer

- 優先以 Wiki 的綜合回答。
- 區分已知、推論、假設、衝突與未知。
- 可驗證主張附內部來源連結或外部引用。
- 視需要產生比較表或視覺輸出，但持久核心結論仍須走正確保存 workflow。

## Persist gate

回答後明確判定是否產生值得保存的新成果。跨情境可重用、綜合多頁、形成新比較／機制／關聯／問題框架、改變既有理解，或使用者明確要求保存，通常值得；一次性操作、純格式轉換、無新增價值的重述與未成熟想法通常不值得。

判定為保存時建立暫時 handoff，說明內容、理由、可更新的既有頁、預計權威位置與授權狀態，再依類型交回 Router：

- reusable knowledge → [[90_System/Workflow Specs/Integrate]]。
- source-specific correction、推導、術語或適用條件 → [[90_System/Workflow Specs/Register and Ingest]] 的既有 Source Note 更新分支，並先回原件核對。
- project-local outcome、狀態或決策 → [[90_System/Workflow Specs/Project]]。
- system behavior gap → [[90_System/Observations]]；已成熟且獲核准時再走 System Decision／Refactor。

沒有涵蓋本次成果的保存授權時，只提出 handoff，不先建草稿或改索引。已有明確授權時，完成本 block Verify 後可直接重路由，不重複詢問。來自 Project 的內容要同時說明是否符合 Integrate 的 Project-origin 條件。

## Write

本 block 無 substantive write。只有 system behavior gap 可依既有權限新增或累加 Observation；這不代表問答成果已被保存。

## Verify

- 回答的證據可追溯，且未把 Project 狀態當成通用知識。
- 已明確給出 persist／do-not-persist 判定與一句理由。
- 需要保存時，handoff 已分類到唯一後續 writer 並標明授權；尚未授權時沒有提前寫入。
- 需要持久化的問答成果不會由 Query 自行改 Knowledge、Source Note、Map、Index 或 Project。

## Approval

回答與判定不需確認；後續寫入依接收 workflow 的 Approval。
