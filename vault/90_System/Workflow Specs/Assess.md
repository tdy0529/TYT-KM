---
id: SYS-WF-ASSESS
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Assess Workflow
---

# Assess

## Trigger

- 需要理解、解釋或評估尚未進入知識庫的外部材料，包括專案中新遇到的文章、影片、資料集或報告。
- 來源成本高、可信度不明，或只可能回答局部問題。

判準是材料位置：未登記外部材料走 Assess；Wiki 本身足以回答才走 Query。同一未登記材料的後續追問若仍依賴該材料，仍是 Assess。暫時移除材料後，Wiki 足以回答則走 Query；不足則走 Assess；兩者都需要時，先完成 Assess Verify，再重路由 Query。

「庫內」包括已登記的 10_Sources 原件，以及 20_Knowledge 的 Notes、Maps、Source Notes。00_Inbox 與專案暫用但未登記的材料仍屬庫外；30_Projects 的頁面是專案狀態，不是通用證據。文件長度本身不改變路由。

## Read

先讀最低必要範圍：來源資訊、摘要／導言／目錄／結論、和問題相關的段落、關鍵圖說或圖表，以及目前問題或 Project Context。判斷 Novelty 時只讀 [[20_Knowledge/Knowledge Index]]，除非需要比較才下鑽。

長文件依 [[AGENTS]] 的長文件規則：可先解析全部頁面建立章節索引，但只把必要範圍帶入分析，並分開回報已抽取、已核對、未核對與建議閱讀範圍。

## Decide

評估 Fit、Authority、Novelty、Actionability、Cost。

## Output

理解面至少回答：材料要解決什麼、核心方法或主張、主要證據及強度、作者限制、明確標為推論的補充限制、實際讀取範圍。

評估面至少回答：適配度、可用於何處、主要落差、建議閱讀範圍、建議處置（丟棄／暫用／Register／完整 Ingest／Query）。使用者只問其中一面時可以縮短另一面，但不能完全省略。

## Assess handoff

同一材料經多輪 Assess，且使用者要求保存、詢問保存方式，或 Register／Ingest Trigger 已成立時，在目前工作鏈建立暫時 inventory；不另建檔，也不保存逐字對話。分類為：

- source claim：來源明示且可附 locator。
- source-specific inference：由來源推導但非作者明示。
- reusable synthesis：可跨來源或情境重用。
- user judgment：使用者的價值、適用性或優先序判斷。
- open question：值得保留的未知。
- discard：重複、已推翻或只有對話過程價值。

依既有授權分流：

1. 未授權保存：只回報分類與預計落點。
2. 只授權保存來源：重路由 Register／Ingest，讓 Source Note 回收 source claim、source-specific inference 與相關 open question；reusable synthesis 只列為 Integrate 候選。
3. 授權來源與可重用知識：先完成 Register／Ingest Verify，再重路由 Integrate；高影響語意仍遵守其 Approval。

user judgment 必須保留角色，不能改寫成來源主張。先前對話無法取得時揭露 handoff 缺口。

材料先做一般 Assess、後來才連到既有 Project 時，先讀 Context，再對已讀範圍與必要原文做 project-relative delta assessment：判斷支持哪個目標、改變哪些限制或設計、留下哪些證據缺口。不得只搬運一般摘要，也不因此自動取得 Register 或 Integrate 授權。

## Write

- 單次短評預設留在對話；沒有既有 Project 時不因 Assess 建立正式頁面。
- 已有 Project 且產生會影響未來判斷、執行或證據解讀的不重複成果時，依 [[90_System/Workflow Specs/Project#Project discussion handoff]] 分流。
- 評估出保存價值不等於已獲來源寫入授權。
- 庫外材料的判讀若寫入持久頁面，必須記錄可識別出處、read scope 與未登記狀態。

## Verify

- 已同時交代理解、評估與讀取範圍。
- 來源主張、推論與使用者判斷已分開。
- handoff 中有未來價值的項目都有分類；已授權項目交給正確 workflow，未授權項目沒有先寫入。
- late-bound Project 情境已完成 delta assessment，無法恢復的脈絡已揭露。

## Approval

Assess 本身不需確認；下載、付費、登入、對外操作、大量 ingest 或後續持久寫入另依相應權限處理。
