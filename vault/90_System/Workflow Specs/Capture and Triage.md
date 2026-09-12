---
id: SYS-WF-CAPTURE-TRIAGE
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Capture Workflow
  - Triage Workflow
---

# Capture／Triage

## Trigger

- 使用者提供資訊、檔案、連結或零散想法，但尚未要求深入處理。
- Obsidian 在 00_Inbox 建立新筆記或附件。

## Read

- 輸入本身。
- 看似屬於既有專案時，讀該 Project Context。

## Decide

- discard：沒有保留價值。
- project-local：只服務一個專案。
- source-candidate：值得評估或登記為可引用來源。
- knowledge-candidate：可能可重用，但仍需驗證依據。

## Write

- 未決內容留在 00_Inbox。
- project-local 依 [[90_System/Workflow Specs/Project]] 寫入 Worklog 或 Output。
- source-candidate 與 knowledge-candidate 只標示候選；是否 Assess、Register 或 Integrate 由 Router 重新判斷。

## Verify

- Inbox 項目已有清楚下一步或已移出。
- 未判定內容沒有被當成正式證據。

## Approval

只有刪除內容，或分流會改變既有重要語意時需要確認。
