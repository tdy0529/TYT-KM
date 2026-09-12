---
id: SYS-005
type: system-decision
status: accepted
created: 2026-09-10
updated: 2026-09-10
aliases:
  - 專案討論交接決策
affects:
  - "[[90_System/Workflows]]"
  - "[[90_System/Metadata Schema]]"
  - "[[90_System/Templates/Project Context Template]]"
  - "[[90_System/Templates/Project Worklog Template]]"
  - "[[90_System/Templates/Project Decision Template]]"
  - "[[90_System/Templates/Source Assessment Template]]"
---

# SYS-005 — Preserve Project Discussion Outcomes

## Context

既有 Project workflow 會先讀 Context，能讓一開始就以專案為目標的文章 Assess 保持 project-aware；但它只明文要求在 Assess 改變下一步或決策時寫 Worklog，也沒有處理文章先做一般 Assess、後來才連到專案的 late-bound 情境。這會讓候選方法、被排除的替代方案、證據缺口、設計含義與使用者判斷等重要精髓只留在聊天。

同時，既有 Context 只要求保存最新狀態，沒有要求指出詳細推理位於哪份 Worklog、Decision、Output、Source 或 Knowledge；「下一次只讀 Context 能恢復」因此可能只恢復到一句摘要，無法找到其依據。Decision 也缺少獨立成頁門檻，可能過度建立或漏記高影響選擇。

使用者於 2026-09-10 明確同意建立 Project discussion handoff、late-bound Assess → Project 交接、Context 可恢復性連結與 Decision 建立門檻。

## Decision

每個產生未來價值的專案工作階段在結束前執行 Project discussion handoff。handoff 是暫時 inventory，不是新檔案或逐字稿；內容分類為 current state、session result、project-specific inference、proposed／accepted decision、source evidence、output change、open question、promotion candidate 或 discard，並分流至 Context、Worklog、Decision、Output、Source Note 或 Promote 候選的權威位置。

Worklog 門檻改為：討論形成不重複成果，且會影響未來專案判斷、執行或證據解讀。它包含但不限於新限制、候選方法、被排除的替代方案、證據缺口、設計含義、決策、未解問題與 promotion candidate；不再要求已經改變下一步或正式決策。

材料先完成一般 Assess、後來才指定用於既有 Project 時，必須先讀 Project Context，再做 project-relative delta assessment；不得只搬運一般摘要。若先前脈絡不可取得，依可重讀的來源重建並揭露缺口。這個交接不自動授權 Register 或 Integrate。

Project Context 必須有 handoff reading path，連到恢復工作所需的 Worklogs、Decisions、Outputs、Sources 與 Knowledge，且每個連結說明用途。獨立 Decision 只在選擇排除其他合理選項、限制後續工作、實質影響成本或風險，或理由必須跨工作階段可恢復時建立；小型可逆操作選擇留在 Worklog 或 Context，accepted 仍只由使用者明確授權。

## Rationale

- 專案真正需要保存的是會改變後續判斷的成果，不是逐字聊天，也不只是 next action。
- Context 應作為可恢復的控制面；詳細推理與證據留在各自權威頁，避免內容重複與漂移。
- 一般文章理解和 project-relative implication 是兩個不同問題；late-bound delta assessment 能補上後者而不假裝先前摘要已經 project-aware。
- 明確的 Decision 門檻同時降低小事過度文件化與重大選擇無理由可追溯的風險。

## Alternatives

### 所有專案討論都保存逐字稿

未採用。逐字稿含重複、探索性分支與已撤回想法，會降低恢復效率，也違反原始對話預設不保存的規則。

### 只在 next action 或正式決策改變時保存

未採用。這會漏掉尚未形成決策、但會影響後續設計與證據解讀的候選方法、反例、限制與缺口。

### Context 納入所有細節

未採用。Context 會快速膨脹並與 Worklog、Decision、Source Note、Output 形成多份真相；reading path 可在精簡與可恢復之間取得平衡。

### 一般 Assess 摘要直接附到 Project

未採用。一般摘要沒有專案的目標與限制作為判斷條件，無法可靠回答材料如何改變專案。

## Consequences

- 重要專案討論不再以「是否立即改變 next action」作為唯一保存門檻。
- Context 增加少量導航維護成本，但下一個工作階段可找到必要推理與證據。
- 同一外部材料可能先有一般 Assess，再有 project-relative delta；只有需要持久引用時才依既有規則 Register。
- Project 頁只保存來源對專案的影響；已登記來源主張仍以 Source Note claim 為 canonical truth。
- 尚未由使用者接受的方案仍保持 proposed。

## Migration

- 更新 Assess 與 Project workflow 的 late-bound 交接、Worklog 門檻、handoff inventory、Decision 門檻與 Verify。
- 更新 Metadata Schema 的 Project Context、Decision 與 Worklog 正文要求。
- 更新 Project Context、Project Worklog、Project Decision 與 Source Assessment 模板。
- 不回溯重寫既有 Project 頁；在其下次實質更新時補上或整理 handoff reading path。

## Rollback

- 移除 Project discussion handoff 與 late-bound delta assessment 條款。
- 還原 Worklog 寫入門檻、Context 必要段落與 Decision 建立門檻。
- 還原四份 Project 模板；已依本決策新增的歷史專案紀錄保留，不自動刪除。

## Revisit when

- Worklog 因門檻過寬而出現大量低價值紀錄。
- Context reading path 維護成本高於恢復效益，或可由可靠的自動索引取代。
- 同一材料跨多個 Project 時出現重複 delta assessment。
- Project discussion handoff 經常需要跨工作階段的獨立 staging type。
