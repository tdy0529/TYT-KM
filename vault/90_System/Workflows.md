---
id: SYS-DOC-WORKFLOWS
type: system-doc
status: reviewed
created: 2026-09-03
updated: 2026-09-10
aliases:
  - 系統工作流
  - Workflow Index
---

# Workflows

本頁是 workflow 路由索引與共同契約，不承載各流程的完整規則。先依 [[90_System/Router Contract]] 選出目前 Trigger，再只讀下表對應規格；不要預先載入其他 workflow。生命週期邊界見 [[90_System/Architecture]]，寫入驗證見 [[90_System/Execution and Verification Contract]]，資料契約見 [[90_System/Metadata Schema]]。

## 共同契約

每份 workflow spec 定義 Trigger、Read、Decide、Write 或 Handoff、Verify、Approval。跨 workflow 的拆解、重路由與停止只由 Router Contract 決定；規格提到後續流程不代表可以自動執行。

「一次工作階段」是從使用者提出一個目標，到 Router 判定完成、no-op、defer、reject、需人決定或 blocked 為止，不以對話輪數或視窗是否關閉判斷。

所有寫入都以局部 lint 為共同 postcondition；完整 lint 的觸發與檢查見 [[90_System/Workflow Specs/Lint and Refactor]]。需要留下系統紀錄的事件依 [[90_System/Execution and Verification Contract#日誌]] 處理。

## 路由索引

| 使用者目前要完成的事                     | Workflow spec                                    | 邊界提示                                                              |
| ------------------------------ | ------------------------------------------------ | ----------------------------------------------------------------- |
| 保存或分流尚未判定的輸入                   | [[90_System/Workflow Specs/Capture and Triage]]  | Inbox 內容不是可靠證據                                                    |
| 理解或評估庫外材料                      | [[90_System/Workflow Specs/Assess]]              | 未登記材料的後續追問仍是 Assess                                               |
| 穩定登記來源並擷取內容                    | [[90_System/Workflow Specs/Register and Ingest]] | Source Note 是單一來源的解讀                                              |
| 將來源、Query 或 Project 候選編譯進 Wiki | [[90_System/Workflow Specs/Integrate]]           | Knowledge 的唯一 substantive writer；Promote 是 Project-origin profile |
| 從庫內回答並判斷成果是否值得保存               | [[90_System/Workflow Specs/Query and Persist]]   | Persist 只分類與取得授權，不直接寫 Knowledge                                   |
| 建立或繼續有持續目標的工作                  | [[90_System/Workflow Specs/Project]]             | 專案狀態不是通用知識                                                        |
| 檢查或重構 Vault                    | [[90_System/Workflow Specs/Lint and Refactor]]   | Lint 檢查；Refactor 才改結構                                             |

斜線相連的名稱是同一個 block 內的階段。Promote 不再是獨立 workflow；它是 Integrate 接收 Project 候選時的資格檢查與 provenance 規則。

## 最小載入

- 日常任務：Router Contract → 本頁 → 一份命中的 workflow spec。
- Query／Integrate：再讀 [[20_Knowledge/Knowledge Index]]，沿 Index、Maps、搜尋與連結逐層縮小。
- Project：先讀對應 Context，再沿 handoff reading path 取得必要依據。
- 寫入：再讀 Execution and Verification Contract；只有用到 type 或欄位時才讀 Metadata Schema 的相關段落。
- System change：依受影響節點載入，而非固定讀完所有核心文件：路由改動讀 Router＋受影響 workflow；流程行為讀本頁＋該 spec＋Execution；欄位或 type 讀 Metadata 對應段落＋模板；生命週期或區域改動才讀 Architecture；另讀直接相關 Decisions／Observations。
- Lint：局部 lint 只讀變更檔與一階鄰接頁；完整 lint 才掃描全 Vault。

不要為了盤點可能路徑而一次載入所有 workflow 或整個 Vault。
