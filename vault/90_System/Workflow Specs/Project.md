---
id: SYS-WF-PROJECT
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Project Workflow
---

# Project

## Trigger

- 使用者明確要求建立或繼續 Project，或已有對應 Context。
- 任務有持續目標，確實需要跨工作階段保存狀態、決策、實驗或交付物。

單次文章理解、格式轉換或可直接回答的問題，未明確要求時不建立 Project。

## Read

先讀 Context，再沿 handoff reading path 讀完成本次目標所需的 Worklogs、Decisions、Outputs、Knowledge 與 Sources。不存在時，才依下節建立最小 draft Context。

## 建立

最小專案只建立 `{Project Name} - Context.md`；Decisions、Worklogs、Outputs 按需建立。Context 至少包含 Objective、Done、Current state、Constraints、Knowledge and sources、Decisions、Open questions、Promotion candidates、Next action 與 Handoff reading path。

## 每次工作階段

1. 讀 Context 並確認本次目標。
2. 搜尋 Knowledge，避免重做。
3. 遇到新材料走 Assess；先前只有一般 Assess 時做 project-relative delta assessment。
4. 來源真正影響決策或會重複使用時才考慮 Register；未登記材料留在專案時仍記錄出處、read scope 與未登記狀態。
5. 結束前執行 discussion handoff，更新 Context 的 current state、next action、reading path 與 promotion candidates。

## Project discussion handoff

有未來價值的討論成果先做暫時 inventory，再分流：

- current state → Context。
- session result、project-specific inference、被排除的替代解釋 → Worklog。
- 達到門檻的 proposed／accepted decision → Decision 並由 Context 連結；只有使用者明確接受才是 accepted。
- source evidence → 連 Source Note claim；未登記時記出處與 read scope。Project 只寫它如何影響專案，不複製來源真相。
- output change → Output；Worklog 只記變更與理由。
- open question → 影響恢復的放 Context，細節放 Worklog並由 Context 連結。
- promotion candidate → Context；是否寫 Knowledge 交由 Integrate 的 Project-origin profile。
- discard → 重複、撤回、無未來價值或只有對話過程的內容不寫。

Worklog 門檻：成果不重複，且會影響未來專案判斷、執行或證據解讀。可續寫同一明確工作階段的 Worklog；目標或決策脈絡改變時新建。

Context 的 handoff reading path 只連恢復工作所需的詳細頁，且每個連結說明為何要讀；Context 不複製細節。

## Decisions

選擇排除其他合理選項、限制後續工作、實質影響成本或風險，或理由必須跨工作階段恢復時，建立獨立 Decision。小型可逆選擇留在 Worklog 或 Context。

## Write

依 handoff 更新 Context，並按需建立或更新 Worklog、Decision、Output。對 Knowledge 的任何 substantive write 一律重路由 Integrate；Project 只維護 candidate 與 provenance。

## Verify

- 下一個 LLM 只讀 Context 即能恢復狀態，並知道沿哪些連結取得依據。
- 重要成果沒有只留在聊天；無後續價值的過程沒有被保存。
- Project inference、source claim、proposed option 與 accepted decision 已分開。
- 專案狀態沒有被誤寫成通用知識；候選知識在 Context 可見。

## Approval

draft Context、Worklog、Output 可依既有權限建立。accepted Decision、需人判斷的泛化與其他高影響動作依 [[AGENTS]] 取得同意。
