---
id: SYS-DOC-METADATA
type: system-doc
status: reviewed
created: 2026-09-03
updated: 2026-09-11
aliases:
  - Metadata Schema
  - 筆記格式規範
---

# Metadata Schema

## Schema 的功能

本文件只規範 type、status、必要 properties、locator 與各類頁面的最低正文契約。實際寫作、關係表達、拆分與合併方法見 [[90_System/References/Authoring and Structure Guidance]]；該指南提供建議與例子，不新增或覆寫正式契約。建立或更新筆記時須讀本文件對應 type 的欄位與正文契約；指南按需載入。模板是建立起點，不是完成證明。

## 通用規則

- 文字編碼：UTF-8。
- 日期：YYYY-MM-DD；需要時間時使用含時區的 ISO 8601。
- YAML 只放可篩選、排序、識別或治理的欄位；長摘要與推理放正文。
- 空列表寫成 []，未知值留空或明確寫 unknown；不得捏造。
- properties 中的內部連結使用加引號的 Wikilink。
- tags 不承擔 type、status、topic 的重複功能。主題優先使用 Maps。
- 每個正式 Markdown 頁面必須有全 Vault 唯一 id。
- Templates 與暫存 Inbox 草稿可在建立當下含 placeholder，但進入正式區前必須替換。
- 模板中的連結 placeholder 使用 {LINK} 或空 property，不可寫成雙中括號的活連結；否則 Obsidian 可能建立錯誤 backlinks 與空白頁。
- 數學一律使用 `$...$`（行內）與 `$$...$$`（區塊），不得使用 `\(`、`\)`、`\[`、`\]`。Obsidian 內建 MathJax 只解析錢字號分隔符，其他分隔符會顯示原始碼；區塊公式前後保留空行。程式碼區塊內的跳脫範例不在此限。

## 通用欄位

| 欄位 | 型別 | 必要 | 說明 |
|---|---|---:|---|
| id | text | 是 | 穩定且唯一；改檔名時不改 id |
| type | enum | 是 | 頁面角色 |
| status | enum | 是 | 依 type 使用允許值 |
| created | date | 是 | 首次建立日期 |
| updated | date | 是 | 最後實質內容更新日期 |
| aliases | list | 是 | 同義詞、常用譯名、舊名；沒有則 [] |

不要把檔案修改時間當成 updated；排版或自動索引變更不一定算實質內容更新。

## ID 與命名

| 對象 | ID | 建議檔名 |
|---|---|---|
| 原始來源與 Source Note | SRC-YYYY-NNNN | SRC-YYYY-NNNN - Title |
| Knowledge Note | KN-YYYY-NNNN | 能獨立表意的標題 |
| Map | MAP-YYYY-NNNN | 主題或問題 - Map |
| Project | PRJ-YYYY-NNNN | 專案名稱 - Context |
| Project Decision | ADR-{PROJECT-ID}-NN | ADR-NN - 決策名稱 |
| Project Worklog | WL-{PROJECT-ID}-YYYYMMDD-NN | YYYY-MM-DD - 工作階段名稱 |
| Project Output | OUT-{PROJECT-ID}-NNN | 可辨識的交付物名稱 |
| System Decision | SYS-NNN | SYS-NNN - 決策名稱 |
| Lint Report | LINT-YYYYMMDD-NN | YYYY-MM-DD - Lint Report |
| 系統錨點 | 保留的語意 ID | 例如 MAP-HOME、IDX-KNOWLEDGE、IDX-PROJECTS |

NNNN 使用該類型下一個未使用編號，不回收舊 ID。

Home、全域 Index、Guide、Log 與 System 文件可使用表意清楚的保留 ID；一般內容頁仍使用流水 ID。

檔名原則：

- 以人可讀、可搜尋為主，ID 留在 property；來源與決策例外，ID 也放檔名。
- 禁止無上下文的 Index.md、Context.md、Notes.md、Log.md。
- 同一概念只有一個 canonical page；其他名稱放 aliases。
- 不在檔名前加資料夾分類碼來表達主題。

## type

允許值：

- knowledge-note
- source-note
- map
- knowledge-index
- project-index
- project-context
- project-decision
- project-worklog
- project-output
- system-doc
- system-guide
- system-decision
- system-log
- system-observations
- lint-report

需要新增 type 時先提出 System Decision，不以自由文字臨時擴充。

## 狀態

### Knowledge Note 與 Map

- draft：已可閱讀，但尚未充分整合或驗證。
- needs-review：需要人的語意判斷。
- reviewed：已在明確範圍內審閱。
- contested：存在未解的可信衝突。
- superseded：被較新頁面取代；正文必須連到替代頁。
- archived：不再主動維護但保留歷史。

### Source Note

- registered：只完成來源登記。
- partial：只讀取部分內容。
- processed：宣稱的範圍已完成擷取。
- superseded：有新版或較佳版本。
- withdrawn：來源被撤回、失效或不應繼續採信。

### Project Context

- active
- paused
- completed
- cancelled

### Project Worklog

- draft
- completed

### Project Output

- draft
- needs-review
- final
- superseded
- archived

### Project Decision 與 System Decision

- proposed
- accepted
- rejected
- superseded

只有使用者明確接受，才能把 decision 設為 accepted。

### Lint Report

- draft
- completed
- superseded

### Index、Guide、Log 與 System 文件

- active
- reviewed
- superseded
- archived

## Knowledge Note 欄位

必要欄位：

    id: KN-YYYY-NNNN
    type: knowledge-note
    kind: concept
    status: draft
    confidence: medium
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    last_verified:
    aliases: []
    maps: []
    source_refs: []
    project_refs: []

kind 允許值：

- concept：定義、機制或原理。
- entity：人物、組織、作品、產品或其他實體。
- method：可重複使用的方法或程序。
- comparison：多個選項或觀點的比較。
- synthesis：跨多來源形成的較大解釋。
- question：仍值得持續累積證據的重要問題。

confidence：

- low：證據有限、來源弱或推論跨度大。
- medium：有合理依據，但仍有重要限制或未驗證處。
- high：多個高品質來源一致，或有直接且可重現證據。

confidence 不是機率，也不因文字寫得肯定就提高。存在可信衝突時通常 status 為 contested。

### Knowledge Note 正文方法

正文至少包含一句話結論、Current understanding、Evidence、Limits and conflicts、Relations、Open questions、Revision history，並回答一個清楚問題。單篇摘要屬 Source Note；專案特例屬 Project；通用結論才屬 Knowledge Note。同一事實只保留一個 canonical 位置：已登記外部數值與來源主張在 Source Note claim，專案最新狀態在 Project Context，通用結論在 Knowledge Note；其他頁面以連結引用，不複製權威正文。

與專案的關聯記於 `project_refs` 與 Relations：`project_refs` 連到相關 Project Context，Relations 說明其為來源情境、應用案例或驗證情境；需要精確 provenance 時，另連到對應 Worklog／Decision／Output。沒有相關專案時 `project_refs` 保持 []，不為填欄位建立專案；專案偶然性與最新狀態不混入通用結論。

外部主張的推薦格式：

    - 主張：清楚且可驗證的句子。
      - 證據：{SOURCE-NOTE-CLAIM-LINK}
      - 角色：support／qualify／contradict
      - 限制：適用條件或未知處

LLM 自己的跨來源推論要明寫「綜合推論」，並列出推論所依賴的主張。使用者觀點寫成「使用者判斷」；專案選擇連到 Decision。

## Source Note 欄位

必要欄位：

    id: SRC-YYYY-NNNN
    type: source-note
    status: registered
    source_type: article
    title:
    authors: []
    published:
    accessed: YYYY-MM-DD
    url:
    raw_path:
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    maps: []
    related_notes: []

source_type 允許值：

- article
- book
- paper
- webpage
- video
- audio
- dataset
- image
- transcript
- conversation
- other

url 與 raw_path 至少應有一項。若原件在 Vault，raw_path 使用從 Vault root 開始的路徑。原始二進位檔不要求 YAML。

### Source Note 正文方法

1. Why this source：為何保留、回答什麼問題。
2. Quick assessment：適配度、權威性、新穎性與主要風險。
3. Read scope：實際讀了哪些頁、章節、時間段或資料範圍。
4. Source summary：忠實表示來源自己的問題、方法與結論。
5. Claim cards：每個可引用主張有 locator 與 block ID。
6. Limitations：來源限制與我們尚未驗證之處。
7. Figures or media：影響理解的圖像、圖表與媒體定位。
8. Connected knowledge：本來源實際更新或支持哪些 Knowledge Notes。

Claim card 格式：

    ### C01 — 簡短主張名

    來源主張：……

    - Locator：p. 12；或 Results > 第 3 段
    - Context：必要的定義、樣本或條件
    - Notes：是否為直接引述、改寫或數值

    ^src-c01

block ID 在同一 Source Note 內唯一。

## Locator 規範

| 來源 | locator |
|---|---|
| PDF／書籍 | 頁碼；必要時章節、表格、圖號 |
| 網頁 | 小節標題＋段落位置；可附 fragment URL |
| 影片／音訊 | HH:MM:SS–HH:MM:SS |
| 資料集 | 版本＋表／欄／列／查詢條件 |
| 圖片 | 檔名＋區域或物件描述 |
| 對話／訪談 | 日期＋說話者＋時間碼或段落 |
| 程式碼 | repository／commit＋檔案＋行號或 symbol |

locator 必須讓另一個人能合理重找，不只是「見文章」。

直接引文保持最少必要長度；一般以準確改寫加 locator 為主。

## Map 欄位與正文

必要欄位：

    id: MAP-YYYY-NNNN
    type: map
    status: draft
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    maps: []

Map 不是資料夾首頁或完整清單。它應包含：

1. Scope：這張 Map 涵蓋與排除什麼。
2. Guiding questions：使用者可以從哪些問題進入。
3. Recommended path：建議閱讀順序及理由。
4. Core notes：每個連結附一行角色說明。
5. Cross-connections：和其他 Map 或領域的關係。
6. Tensions and gaps：衝突、缺口與下一步。

建立門檻：至少 3 篇有實質關係的 Note。Map 只做導航與關係說明，不含 Evidence、confidence 或 claim block。

## Project 欄位

### Project Context

    id: PRJ-YYYY-NNNN
    type: project-context
    status: active
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    knowledge_refs: []
    source_refs: []

正文必須含 Objective、Done、Constraints、Current state、Decisions、Knowledge and sources、Open questions、Promotion candidates、Next action、Handoff reading path。

Handoff reading path 連到恢復工作所需的 Worklogs、Decisions、Outputs、Sources 與 Knowledge，每個連結附一行用途。Context 保存最新狀態與導航，不複製詳細推理、來源主張或交付物正文。

Promotion candidate 狀態使用 candidate、promoted、deferred 或 rejected；deferred 必須寫明證據或泛化缺口。

### Project Decision

    id: ADR-{PROJECT-ID}-NN
    type: project-decision
    status: proposed
    project:
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    source_refs: []

正文必須含 Context、Decision、Options considered、Rationale、Consequences、Revisit when。

只有在選擇排除其他合理選項、限制後續工作、實質影響成本或風險，或理由必須跨工作階段可恢復時，才建立獨立 Project Decision。小型、可逆且不影響後續判斷的操作選擇留在 Worklog 或 Context；只有使用者明確接受才能使用 accepted。

### Project Worklog

    id: WL-{PROJECT-ID}-YYYYMMDD-NN
    type: project-worklog
    status: completed
    project:
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    source_refs: []
    knowledge_refs: []

Worklog 是壓縮後的工作成果，不是聊天逐字稿。當本次討論形成不重複、且會影響未來專案判斷、執行或證據解讀的成果時，保存本次目標、行動、結果、證據、project-specific inference、被排除的替代方案、決策或變更、本次新增的未解問題與 promotion candidates。只重述既有狀態或沒有後續價值的探索不保存；next action 只寫在 Project Context。

### Project Output

    id: OUT-{PROJECT-ID}-NNN
    type: project-output
    status: draft
    project:
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    source_refs: []
    knowledge_refs: []

正文必須含 Purpose、Output、Evidence and dependencies、Limits 與 Promotion candidates。final 表示專案交付狀態，不表示其中每個主張都已成為通用知識。

## System Decision 欄位

    id: SYS-NNN
    type: system-decision
    status: proposed
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    aliases: []
    affects: []

只有 accepted 的 System Decision 能改變正式規則。正文記錄 Context、Decision、Rationale、Alternatives、Consequences、Migration、Rollback、Revisit when。

## 連結方法

正式頁面優先用完整 Vault 路徑的 Wikilink；精確證據連 Source Note block，導航連頁面或 heading。Backlinks 不寫入 YAML。連結在正文中必須說明關係；詳細模式見 [[90_System/References/Authoring and Structure Guidance#連結與關係]]。

## 拆分與合併準則

一頁回答一個可獨立演進的問題；頁面沒有獨立結論或只是同義重複時應考慮合併。判斷方法見 [[90_System/References/Authoring and Structure Guidance#拆分與合併]]。合併、刪除與批次改名先取得確認，並更新所有連入連結或保留 redirect。

## 完成一篇筆記的檢查

完成條件不在 Schema 重複定義；依目前 Workflow Verify、[[90_System/Execution and Verification Contract]] 與 [[90_System/Workflow Specs/Lint and Refactor]] 檢查實際產物。
