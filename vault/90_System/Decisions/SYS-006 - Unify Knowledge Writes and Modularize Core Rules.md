---
id: SYS-006
type: system-decision
status: accepted
created: 2026-09-10
updated: 2026-09-10
aliases:
  - 統一知識寫入與核心規則模組化決策
affects:
  - "[[AGENTS]]"
  - "[[90_System/Architecture]]"
  - "[[90_System/Router Contract]]"
  - "[[90_System/Workflows]]"
  - "[[90_System/Execution and Verification Contract]]"
  - "[[90_System/Metadata Schema]]"
  - "[[90_System/Obsidian Usage]]"
  - "[[90_System/Templates/Project Context Template]]"
  - "[[30_Projects/Projects Index]]"
---

# SYS-006 — Unify Knowledge Writes and Modularize Core Rules

## Context

原本 Integrate、Promote 與 Query／Persist 都能直接建立或更新 Knowledge Note、Map 與 Index，造成三套相似的去重、證據、衝突、核准與同步責任。Promote 雖有必要的 Project 泛化與 provenance 判斷，但其 Knowledge write 和 Integrate 同質；Query 的 Persist 同時判斷「值不值得存」與實際寫入，也繞過 Integrate 的一致規則。

同時，全部八個流程集中在 615 行的 Workflows.md。日常任務即使只命中一個 block，也容易載入其他流程；System change 更固定要求 Architecture、Metadata 與整份 Workflows，和「按需載入」的設計目標矛盾。Architecture、Metadata、AGENTS 與 Obsidian Usage 也混入可按需查閱的規模策略、寫作方法與工具設定。

使用者於 2026-09-10 明確要求先建立 Git 檢查點，再執行合併 Promote／Integrate、收斂 Query Persist、拆分 Workflows 與精簡核心文件。

## Decision

Integrate 成為 20_Knowledge 的唯一 substantive writer，統一接收 Source-origin、Query-origin 與 Project-origin 三種輸入。原 Promote 不再是獨立 workflow，而是 Integrate 的 Project-origin profile，保留 Reusable、Evidence、Generalized、Atomic、Connected、Non-duplicate 條件，以及 integrate／defer／reject 結果、Project provenance 與 candidate 狀態同步。

Query 負責回答；Persist 只判斷新增成果是否值得保存、分類權威落點與確認授權。它不得直接修改 Knowledge、Source Note 或 Project：reusable knowledge 交 Integrate；source-specific enrichment 交 Register／Ingest 更新分支；project-local outcome 交 Project；system gap 交 Observation 或經核准的 System Decision／Refactor。

Workflows.md 改為導航索引與共同契約；各 block 拆到 `90_System/Workflow Specs/`，日常只載入命中的 spec。System change 依受影響節點選讀規則，不再固定載入所有核心文件。

Architecture 只保留生命週期、區域、權威、資料流與審核邊界；規模策略移到 Reference。Metadata 只保留資料契約，寫作與結構判斷移到 Reference。AGENTS 保留啟動順序、硬邊界、權限與完成條件；Obsidian Usage 的 Web Clipper 設定移到按需 Reference。

## Rationale

- 一個 Knowledge writer 能保證所有來源使用相同的頁面邊界、去重、證據、衝突與索引規則。
- Promote 的差異是輸入資格和 provenance，不是另一套寫入機制。
- Persist 是決策閘門；把它與 writer 分離，能讓「回答後建議保存」不等於未經授權寫入。
- workflow 分檔後，context 成本由整份流程手冊改為索引加單一 spec，且每份規則仍有唯一權威。
- Reference 保存低頻但有用的說明，不讓刪減變成資訊遺失。

## Alternatives

### 保留 Promote，只引用 Integrate 的 Write

未採用。雖減少部分文字，Router 仍需在兩個同樣會寫 Knowledge 的 workflow 間選擇，責任邊界沒有真正消失。

### Query／Persist 直接呼叫共用寫入清單

未採用。它仍會同時負責回答、保存判定與寫入，無法獨立驗證授權與 transition。

### 只縮短 Workflows，不分檔

未採用。所有流程仍共享一個載入單元，後續新增規則會再次膨脹。

### 直接刪除低頻說明

未採用。規模策略、寫作方法與工具設定仍有操作價值，移到按需 Reference 較可回復。

## Consequences

- workflow 數量由八個降為七個；Promote 仍可作為使用者語彙與 Integrate alias，但不是 Router block。
- persisted query 與 promote 日誌名稱停止新增；實際 Knowledge write 統一記為 integrate。歷史日誌不改寫。
- 既有指向 Workflows 章節的連結需要改到對應 spec；歷史 Decisions 與 Logs 保留當時用語。
- 新增多份短 spec，但日常載入總量下降；跨流程任務仍依 Router 逐 block 載入。

## Migration

- 先以 Git commit `9e8965c` 保存 SYS-005 檢查點。
- 建立七份 Workflow Specs，將 Workflows.md 改為索引。
- 將 Promote 規則合併至 Integrate；改寫 Query／Persist 的 Handoff 與 Verify。
- 更新 AGENTS、Architecture、Router、Execution、Metadata、Project Index、Knowledge 入口、Inbox Guide、Obsidian Usage 與 System Map 的現行引用；建立寫作、規模與 Web Clipper 三份按需 Reference。
- 歷史 Decisions、Logs 與 Lint Reports 不回溯改寫。

## Rollback

- 以本決策前的 Git 檢查點恢復單檔 Workflows 與三條 Knowledge write 路徑。
- 移除 Workflow Specs 與新增 References，恢復各入口舊連結。
- 不回退其後由新流程建立的 Knowledge；需逐項確認其內容而非機械刪除。

## Revisit when

- 一項合法 Knowledge write 無法由 Integrate 表達。
- Persist handoff 經常遺失回答中的可重用成果。
- workflow spec 間出現重複規則或跨檔載入成本高於原單檔。
- 使用者無法從 Project candidate 狀態辨識 defer、reject 與已整合。
