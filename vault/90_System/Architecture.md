---
id: SYS-DOC-ARCHITECTURE
type: system-doc
status: reviewed
created: 2026-09-03
updated: 2026-09-10
aliases:
  - 系統架構
---

# Architecture

## 目的與不變量

TYT-KM 是通用型 LLM–Obsidian 知識系統，以同一生命週期處理來源、理解、專案與系統演進。核心不變量是：

1. 原始來源是不可任意改寫的證據層。
2. Source Note 保存單一來源的忠實解讀；Knowledge 是可持續修訂的跨來源 Wiki。
3. Project 保存情境性工作，不直接等於通用知識。
4. Schema 與 workflow 是人和 LLM 共用的操作契約。
5. 所有重要外部主張可回到來源與 locator；衝突不被默默抹平。
6. 索引、日誌、lint 與 Git 分別支援導航、語意理由、一致性檢查與版本回復。

成功表示：已整合知識不必每次從原件重建；新資訊能進入既有頁與關係；專案可快速使用未完整入庫材料而不污染 Wiki；例行維護可自動執行，高影響語意仍由人決定。

## 區域

```text
TYT-KM/
├── 00_Inbox/                 未判定輸入
├── 10_Sources/               已登記原始證據
├── 20_Knowledge/             Source Notes、Knowledge Notes、Maps、Index
├── 30_Projects/              Context、Decisions、Worklogs、Outputs
├── 90_System/
│   ├── Architecture.md
│   ├── Router Contract.md
│   ├── Workflows.md           workflow 索引與共同契約
│   ├── Workflow Specs/        按 Trigger 載入的流程規格
│   ├── Execution and Verification Contract.md
│   ├── Metadata Schema.md
│   ├── Templates/
│   ├── Decisions/
│   ├── Logs/
│   ├── References/
│   └── Observations.md
├── AGENTS.md                  啟動入口與硬邊界
└── .obsidian/                 Obsidian 應用設定
```

頂層資料夾表達生命週期與權威，不表達學科。

### 00_Inbox

快速收件與暫存；不能作可靠知識引用。內容應被丟棄、移入 Project、Register 為 Source，或經正確流程形成 Knowledge。

### 10_Sources

保存已登記原件或可重現快照，以 source ID 管理。原件與解讀分離；轉錄、OCR、清理結果要另存並保留關係。

### 20_Knowledge

- Source Notes：單一來源的 read scope、claims、locator、限制與解讀。
- Knowledge Notes：跨來源或跨情境的概念、方法、比較與綜合。
- Maps：問題導向的閱讀路徑與關係。
- Knowledge Index：LLM 的低成本全域檢索入口。
- Knowledge Catalog.base：由 metadata 動態產生的維護視圖。

Knowledge 的 substantive write 只由 Integrate 執行；Register／Ingest 可以建立與更新 Source Note。

### 30_Projects

有限目標的工作記憶。Context 保存最新狀態與 handoff reading path，Decisions 保存高影響選擇，Worklogs 保存會影響後續工作的壓縮成果，Outputs 保存交付物。可重用候選留在 Context，通過 Integrate 的 Project-origin profile 後才進 Knowledge。

### 90_System

控制平面。Architecture 定義生命週期和權威；Router 管理跨 block 控制；Workflows 是載入索引；Workflow Specs 管理 block 內規則；Execution 管理可觀察驗證與日誌；Metadata 管理 type、欄位、狀態與正文契約。Decisions、Logs、Observations、References 與 Templates 只在需要時載入。

## 索引分工

| 元件 | 唯一責任 |
|---|---|
| Knowledge Index | 每頁一行內容摘要，先縮小搜尋範圍 |
| Maps | 有觀點的問題、論證或學習路徑 |
| Knowledge Catalog.base | 依 properties 動態篩選狀態與維護需求 |

三者互相引用但不複製同一份完整真相。

## 知識編譯鏈

```text
外部材料 ─Capture/Assess─> 丟棄／暫用／Register
                              │
                              v
                    Raw Source + Source Note
                              │
Query persist candidate ──────┼──────> Integrate ──> Notes／Maps／Index
Project promotion candidate ──┘              │
                                             v
                                      Lint／Refactor
```

- Capture 保存或分流。
- Assess 在不先入庫的情況下理解與評估材料。
- Register 讓來源可穩定引用；Ingest 理解單一來源。
- Query 回答；Persist 只判斷保存價值、落點與授權。
- Integrate 是 Knowledge 的單一 writer，統一處理 Source、Query 與 Project-origin 輸入。
- Project 維護情境狀態與 promotion candidates。
- Lint 發現問題；Refactor 才改結構。

每個 block 完成 Verify 後，由 Router 依新狀態重判；候選 transition 不會自動執行。

## 權威分工

- [[90_System/Architecture]]：區域、生命週期與內容權威。
- [[90_System/Router Contract]]：拆解、路由、transition 與停止。
- [[90_System/Workflows]]：workflow 導航與共同契約。
- `90_System/Workflow Specs/`：各 block 的 Trigger、Read、Decide、Write／Handoff、Verify、Approval。
- [[90_System/Execution and Verification Contract]]：寫入後的可觀察驗證與日誌。
- [[90_System/Metadata Schema]]：type、欄位、狀態與正文最低契約。

規則只在一個權威位置完整定義；其他文件以連結引用，不複製。

## 連結與權威

- Map → Note：閱讀路徑中的角色。
- Knowledge Note → Source Note claim：證據、限制或反證。
- Knowledge Note ↔ Knowledge Note：前提、機制、比較、衝突或應用。
- Project → Knowledge：使用的通用理解。
- Project → Source：採用的證據。
- Source Note → Raw Source：可重現原件或 URL。

Backlinks 是推導視圖，不需維護完全對稱的清單。連結必須能回答「為何有關」。

## 寫入與審核

- draft 可直接建立與演進。
- needs-review 表示需人判斷或有未解問題。
- reviewed 可補充；改變核心結論前先呈現差異。
- contested 保留可信衝突。
- accepted Decision 只由使用者明確授權。
- 原件不可默默修改。

Git 保存實際版本；System Log 保存變更理由，兩者不互相取代。

## 發行邊界

使用者 Vault 包含本架構列出的規則、模板與內容；開發者內部的測試標準答案、執行紀錄與驗證資料不進入日常載入路徑，也不隨使用者版發行。

## 演進

反覆但未成熟的問題先記 [[90_System/Observations]]；能寫成可驗證規則且成本合理時，再以 System Decision 修改正式契約。規模策略與延後採用的工具見 [[90_System/References/Scaling and Deferred Infrastructure]]；Obsidian 的人機操作方式見 [[90_System/Obsidian Usage]]。

相關決策：[[90_System/Decisions/SYS-001 - Initial Architecture]]、[[90_System/Decisions/SYS-002 - Adopt Router and Verification Contracts]]、[[90_System/Decisions/SYS-006 - Unify Knowledge Writes and Modularize Core Rules]]。
