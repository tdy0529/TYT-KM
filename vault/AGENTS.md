# TYT-KM：LLM–Obsidian 協作規則

## 目標與入口

建立可追溯、可重組、可維護的 Markdown／Wikilink 知識庫。Obsidian 是人類閱讀與校訂的 IDE；LLM 搜尋、整理、連結、綜合與維護。

每次依序：

1. 讀 `90_System/Router Contract.md` 拆解請求。
2. 從 `90_System/Workflows.md` 選出 Trigger 已成立的 workflow，只讀命中的 Workflow Spec。
3. Query／Integrate 先讀 `20_Knowledge/Knowledge Index.md`；Project 先讀對應 Context。
4. 寫入前搜尋同義詞、既有頁與衝突，優先更新。
5. 有寫入時依 `90_System/Execution and Verification Contract.md` 驗證；完成目前 workflow 後重新路由。
6. 只做完成目標所需的最小、可回復變更。

## 區域與權威

- `00_Inbox`：未判定輸入，不可作可靠證據。
- `10_Sources`：已登記原始材料；原件原則上不可改寫。
- `20_Knowledge`：跨情境可重用的 Wiki；一般 Query 的主要依據。
- `30_Projects`：目標、限制、決策、過程與交付物；不是通用知識。
- `90_System`：架構、資料契約、流程、決策與維護紀錄。

## 不可破壞規則

1. 原件與解讀分離：原件在 Sources，單一來源解讀在 Knowledge/Source Notes。
2. 外部主張可追溯到來源與 locator；來源主張、LLM 推論、使用者判斷、決策與暫時觀察要分開。
3. 不掩蓋衝突；並列證據、限制與未知。建議不等於決策，未明確接受時保持 proposed。
4. 原始對話預設不保存；只保存對未來有價值的成果。Project 狀態留在 Project；只有 Integrate 可 substantive write Knowledge。
5. 主題由 Maps、properties、Wikilinks 與 backlinks 表達，不用資料夾複製分類；連結必須能說明關係。
6. 正式檔名與 ID 全 Vault 可辨識且唯一；不建立多個無上下文的 Index、Log、Context 或 Notes。
7. 不在沒有必要時整庫讀取或批次改寫。
8. 長文件可由工具解析全部頁面建立結構索引，但先只回傳章節、頁碼與必要短片段，再按問題擴大。使用庫內長文件時，分開回報已抽取、已核對、未核對與建議閱讀範圍；標題辨識不可靠時要揭露。
9. 暫存與中間產物寫入系統暫存目錄，不進 Vault；Vault root 只保留 Architecture 定義的五區、AGENTS.md 與應用設定。

## 寫入權限

可直接執行：建立或更新 draft；依明確授權 Register／Ingest；建立 Project Context、Worklog、Output 草稿；補齊無歧義 metadata、locator、Wikilink、索引；修正機械 Schema 錯誤；局部 lint 與必要日誌；新增或累加 Observation。

先說明影響並取得同意：刪除、移動或改寫來源原件；合併、刪除、批次改名；需人判斷的 Project 泛化；提出或接受 Decision；改變 reviewed 核心結論；修改 AGENTS.md 或 reviewed 核心規則（Architecture、Router、Workflows／Workflow Specs、Execution、Metadata）。

## 建立、保存與升級

- 新材料可先 Assess；只有值得穩定引用或使用者要求時才 Register。
- Query 回答，Persist 只判斷保存價值、落點與授權；實際寫入重路由至 Register／Ingest、Integrate 或 Project。
- Project 隨時維護 promotion candidates；只有跨情境可重用、證據足夠且已移除專案偶然性的候選，才由 Integrate 寫入 Knowledge。
- 不確定內容留在 Project 或標記 draft／needs-review，不假裝成熟。
- 所有正式筆記遵守 `90_System/Metadata Schema.md`；日期使用 `YYYY-MM-DD`，內部關聯用 Wikilink，外部來源用 URL 或 raw_path。

## 完成條件

每次寫入後執行局部 lint：frontmatter、必要欄位、連結、locator、重複名稱與索引可達性。Ingest、Integrate、完整 lint、實際修復、Refactor 或 system change 依執行契約記入當月 Log。

完成回報必須列出：實際新增／修改檔案、規格未涵蓋而自行決定之處、目前已成立但未執行的 workflow Trigger；另回報待確認與未解衝突。

完整規範見 [[90_System/Router Contract]]、[[90_System/Workflows]]、[[90_System/Execution and Verification Contract]]、[[90_System/Metadata Schema]]、[[90_System/Architecture]]。
