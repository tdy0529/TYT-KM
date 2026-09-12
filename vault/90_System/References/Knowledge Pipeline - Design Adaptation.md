---
id: SYS-REF-KNOWLEDGE-PIPELINE
type: system-doc
status: reviewed
created: 2026-09-03
updated: 2026-09-11
aliases:
  - Knowledge Pipeline 設計適配
---

# Knowledge Pipeline — Design Adaptation

本頁記錄初始設計依據，採用脈絡見 [[90_System/Decisions/SYS-001 - Initial Architecture]]；現行操作以 [[90_System/Architecture]]、[[90_System/Router Contract]] 與 [[90_System/Workflows]] 所連的 Workflow Specs 為準。

本頁記錄從使用者提供的 knowledge-pipeline 資料夾採納、修改與未採納的設計，避免日後誤以為兩套系統完全相同。

## 採納

- System、Knowledge、Projects 的責任分離。
- Project Context 保存可恢復狀態。
- Decision 與一般筆記分離，且 proposed 不等於 accepted。
- 專案產物經 promotion 才成為通用知識。
- 先記 Observation，重複出現後才升級成規則。
- Workflow 以 Trigger、Read、Write、Done 等條件明確描述。

## 修改

- 從特定研究方法 pipeline 改為通用知識生命週期。
- 不以工作目錄或方法家族決定路由，而以 prompt 意圖、type 與 Project Context 決定。
- raw evidence 擴大為文章、書籍、網頁、影音、資料集、對話與個人觀察。
- promotion 採增量觸發，不等專案結束。
- 新文章先 Assess，無需完整 ingest 才能在專案中試用。

## 未採納

- 綁定 PDF、表格或特定研究階段的固定 pipeline。
- 為尚未出現的資料格式預建大量空目錄。
- 初始就加入執行器、批次腳本或外部檢索服務。
- 把所有工作紀錄自動升級為知識。

## 原因

借用結構性原則，但不借用領域假設。只有在實際材料與任務反覆證明有需要時，才把某一類專門 pipeline 加回系統。
