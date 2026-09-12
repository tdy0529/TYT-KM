---
id: SYS-DOC-OBSIDIAN
type: system-doc
status: reviewed
created: 2026-09-03
updated: 2026-09-11
aliases:
  - Obsidian 使用方式
---

# Obsidian Usage

## 核心協作迴圈

    你在 Obsidian 瀏覽、追問、校訂
              ↓
    你把問題、來源或目標交給 LLM
              ↓
    LLM 依 AGENTS、Schema、Workflow 搜尋與寫入
              ↓
    Obsidian 即時顯示 properties、links、backlinks、Base 與 graph
              ↓
    你沿連結檢查推理，決定下一個問題或是否接受變更

LLM 的設定不只是檔案路由。它同時規定書寫格式、證據方法、頁面拆分、狀態轉移、跨頁同步與審核邊界。Obsidian 讓這些結果可視、可導航、可修正。

## 啟動入口

1. 一般瀏覽從 [[20_Knowledge/Home]] 開始。
2. 搜尋內容先看 [[20_Knowledge/Knowledge Index]] 或使用 Quick Switcher。
3. 看狀態、草稿與來源筆記時開啟 [[20_Knowledge/Knowledge Catalog.base]]。
4. 做專案時從 [[30_Projects/Projects Index]] 進入該 Project Context。
5. 丟入未分類材料時使用 00_Inbox；附件自動進入 _attachments。

## Properties

Properties 是機器與人共享的控制平面：

- type 決定頁面角色。
- status 決定成熟度與審核狀態。
- kind 區分知識形態。
- maps、source_refs、project_refs 連接導航、證據與來源情境。
- updated、last_verified 支援維護與時效檢查。

不要把完整摘要、推理或引文塞進 property。這些內容不適合在表格中閱讀，也會讓 YAML 難以維護。

在 Obsidian 的 Properties view 中，可以檢查是否出現拼字近似但不同的欄位；例如 source_ref 與 source_refs 同時存在就是 Schema 漂移。

## Wikilinks、Headings 與 Block references

- 頁面層連結：連到整個概念或來源。
- Heading 連結：連到一個穩定章節。
- Block reference：連到 Source Note 中可精確引用的 claim。
- Alias：讓同一 canonical page 以自然語言出現在不同句子。
- Embed：在另一頁呈現同一內容，避免複製後形成兩份真相。

LLM 寫連結時要在句子中說明關係。只有 Related links 清單通常不夠。

在 Obsidian 內改名正式筆記時，保持「自動更新內部連結」開啟；批次改名仍應先由 LLM 搜尋所有連入連結並說明影響。

## Backlinks 與 Outgoing links

閱讀一篇 Knowledge Note 時：

- Outgoing links 顯示這頁主動依賴或指向什麼。
- Backlinks 顯示哪些頁面正在使用它。
- 更新核心結論前，先查看 backlinks，可找出可能要同步的下游頁。
- Unlinked mentions 可發現尚未建立的關係，但只在語意成立時轉成 link。

Backlink 只表示被提及，不自動表示支持、因果或同意。

## Graph View 與 Local Graph

全域 Graph 適合觀察：

- 是否有大量孤兒頁。
- 哪些頁面成為過度集中的樞紐。
- Maps 是否真的連接主題。
- 來源群與知識群是否只有單向、薄弱的關係。
- 不同領域之間是否出現有意義的橋接頁。

Local Graph 適合回答「這頁的一到兩階鄰居是否合理」。一般校訂比全域 Graph 更常用。

目前 graph 已按 Inbox、Sources、Knowledge、Projects、System 設定顏色，並顯示箭頭與孤兒。Graph 是診斷工具，不是品質分數；連結越多不一定越好。

## Knowledge Catalog.base

Base 使用 frontmatter 即時計算，不要求額外社群外掛。內建 views：

- 綜合知識：所有 Knowledge Notes。
- 待複核：draft、needs-review、contested。
- 來源筆記：所有 Source Notes。
- 知識地圖：所有 Maps。

source count 由 source_refs 動態計算。Base 可以排序、篩選、分組與直接編輯 properties。

注意：

- Base 的動態列出不等於完成 Knowledge Index 的一行摘要。
- 在表格直接改 status 仍須遵守審核規則。
- Base 沒有顯示正文中的證據品質；需要開啟頁面檢查。

## Knowledge Index 與 Maps

Knowledge Index 是 LLM 的低成本檢索入口。它讓 LLM 先看數百字的頁面摘要，再決定讀哪些全文，符合 LLM Wiki 在中小規模避免每次重新搜尋原始文件的做法。

Map 是有觀點的導航，不是字母排序：

- 一張 Map 可表示學習順序。
- 一張 Map 可表示論證結構。
- 一張 Map 可把相同筆記放在另一個領域脈絡。
- 建立 cross-connections 時，要寫出兩邊透過什麼問題相連。

## Templates

Obsidian 的 Templates folder 已設為 90_System/Templates。

手動建立筆記時：

1. 先在正確位置建立具辨識度的檔名。
2. 執行 Insert template。
3. 替換 ID 中的 NNNN 或 NN。
4. 刪除不適用的 placeholder。
5. 依 Metadata Schema 完成內容。

LLM 建立頁面時同樣遵守模板語意，但不需要機械保留所有空段。

## Search

常用搜尋方向：

- 限定知識區：path:"20_Knowledge"
- 尋找待複核：property status 為 needs-review
- 尋找某來源 ID：搜尋 SRC-YYYY-NNNN
- 尋找未完成 placeholder：搜尋 NNNN 或 TODO
- 尋找沒有進入 Map 的筆記：優先用 Knowledge Catalog 檢查 maps 空值

Quick Switcher 適合已知名稱；Search 適合正文；Base 適合結構化 properties；Knowledge Index 適合先理解有哪些頁。不要用單一工具硬做所有檢索。

## Canvas 與 Excalidraw

- Canvas 適合空間式比較、系統圖、論證或專案規劃。
- Excalidraw 適合手繪推理、視覺註解與概念草圖。
- 圖像中的關鍵結論、來源與限制仍應回寫 Markdown。
- Canvas 中優先嵌入既有 Note，而不是複製其文字。

## Web Clipper 與附件

Web Clipper 的唯一預設職責是 Capture：把網頁轉成可由人與 LLM 讀取的 Markdown 來源候選。它不負責判斷可信度，也不直接建立正式 Source Note 或 Knowledge Note。

設定、模板欄位、Highlighter／Interpreter 選擇、圖片限制與從剪藏到 Register 的操作見 [[90_System/References/Web Clipper Setup]]。實際生命週期仍以 Capture、Assess 與 Register／Ingest workflow 為準。

## 日常使用的最小習慣

- 有東西先丟 Inbox，不先想分類。
- 問 LLM「這值得讀多少？」再決定是否完整 ingest。
- 讀 Knowledge Note 時沿證據 block 抽查。
- 做專案前讓 LLM 讀 Context。
- 工作階段結束讓 LLM 更新 Context 的 next action 與 promotion candidates；符合條件時由 Integrate 編譯進 Knowledge。
- 定期看待複核 Base，不需要每天整理全庫。

## 不要誤用

- Graph 漂亮不代表內容可靠。
- Properties 完整不代表摘要正確。
- Source Note 不是跨來源知識。
- Worklog 不是長期 Wiki。
- LLM 的流暢文字不是證據。
- Sync 是同步，不等於完整版本治理；Git 與備份仍有不同用途。
