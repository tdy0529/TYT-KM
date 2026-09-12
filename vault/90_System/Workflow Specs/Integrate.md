---
id: SYS-WF-INTEGRATE
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Integrate Workflow
  - Promote Workflow
---

# Integrate

Integrate 是 20_Knowledge 的唯一 substantive writer。來源 ingest、Query synthesis 與 Project promotion 使用同一套頁面邊界、去重、衝突與索引規則；來源不同只改變進入資格、證據與完成後要同步的 provenance。

## Trigger

- Source Note 或新證據會支持、限制、取代、反駁或連結現有理解。
- Query／Persist 已辨識值得保存且已授權的跨情境 synthesis。
- Project promotion candidate 已提出，且使用者目標仍包含判斷或保存通用知識。

候選存在不等於自動寫入；Router 仍需確認本次目標、授權與前一 workflow Verify。

## Read

1. [[20_Knowledge/Knowledge Index]]。
2. 命中的 Maps、Knowledge Notes、Source Notes 與必要 locator。
3. 目前 handoff：Assess 的 reusable synthesis、Query 的 persist candidate，或 Project Context 中的 promotion candidate 及其 Worklog／Decision／Output provenance。
4. 同義詞、aliases、既有主張、backlinks 與可能衝突。

handoff 是輸入摘要，不取代來源證據或原專案紀錄。

## Input profiles

### Source-origin

以 Source Note claims 為外部證據；判斷它們如何改變既有 Wiki。

### Query-origin

只接收 Query／Persist 已分類、已授權且可跨情境重用的成果。保留其所依賴的 Knowledge／Source links；若只是 Source Note 缺少來源特定推導或限制，應回 Register／Ingest 更新分支，不由 Integrate 複製。

### Project-origin（原 Promote）

先同時檢查：

1. Reusable：能在原專案外使用。
2. Evidence：有來源、可重現觀察或清楚推理鏈。
3. Generalized：已移除專案名稱、特定限制與偶然細節。
4. Atomic：回答一個清楚問題。
5. Connected：能連入既有 Map／Notes。
6. Non-duplicate：優先更新既有頁。

資格結果為：

- integrate：通過門檻，進入下方 Decide／Write。
- defer：可能有價值但證據或泛化不足；不寫 Knowledge，在 Project candidate 留下缺口。
- reject：只對該專案成立；不寫 Knowledge，保留為 Project 紀錄。

## Decide

先列出材料形成的獨立問題。若無法舉出會只更新其中一題、而不更新其他題的具體證據，應合併為同一問題。對每個問題與 claim 選擇：

- strengthen：增加證據。
- qualify：加入條件或限制。
- contradict：保留可信衝突。
- supersede：較新或較強證據取代舊資訊。
- connect：建立有解釋力的跨頁關係。
- create：現有頁無法合理承載時才新建。
- no-op：既有內容已涵蓋且沒有新價值。

## Write

- 優先更新既有 Knowledge Note；新頁只承載真正獨立的問題。
- 外部可驗證主張連到 Source Note claim block；Query synthesis 保留其依賴；Project-origin 保留原 Project provenance，但不複製 Worklog 原文。
- 必要時更新 Map，並用一句話說明關係。
- 同步 Knowledge Index 的摘要、狀態與 updated。
- 衝突並列證據、locator、適用範圍與目前判斷，不默默抹平。
- Project-origin 完成後更新 Context candidate 狀態為 promoted／deferred／rejected；使用 deferred 而非把證據不足的內容假裝成熟。
- 依執行契約記錄 integrate。日誌不再另分 promote 或 persisted query。

變更多寡由語意影響決定，不追求固定頁數。

## Verify

- 新資訊已進入既有知識網路，且沒有重複概念頁。
- 頁面邊界、連結、證據、限制、衝突與 status 一致；局部 lint 通過。
- handoff 中已授權的 reusable synthesis 已寫入，或以 no-op／defer／reject／需核准明確結案，沒有只留在聊天。
- Project-origin 保留 provenance 並同步 candidate 狀態；專案偶然性沒有混入通用結論。

## Approval

- draft 的一般整合可直接執行。
- 改變 reviewed 核心結論、選擇互斥解釋、把 contested 改為 reviewed，或 Project 泛化涉及價值判斷、偏好、策略承諾或跨場景誤導風險時，先呈現差異與證據。
