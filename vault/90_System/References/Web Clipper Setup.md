---
id: SYS-REF-WEB-CLIPPER
type: system-guide
status: active
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Web Clipper 設定
---

# Web Clipper Setup

本頁是工具設定參考，不定義來源生命週期。權威流程見 [[90_System/Workflow Specs/Capture and Triage]]、[[90_System/Workflow Specs/Assess]]、[[90_System/Workflow Specs/Register and Ingest]]。

## 基準設定

使用 `90_System/Templates/Web Clipper/TYT-KM - Web Source Candidate.json`：

- Vault：`TYT-KM`
- Behavior：Create a new note
- Note location：`00_Inbox/Web Clips`
- Note name：`{{time|date:"YYYY-MM-DD HHmmss"}} - {{title|safe_name}}`
- Trigger：HTTP／HTTPS；網站專用模板排在本模板之前
- Properties：`source_type`、`title`、`authors`、`published`、`accessed`、`url`、`created`、`updated`
- Content：來源警示、來源資訊與 `{{content}}`；不另存可能重複或截斷的 `{{description}}`

Capture 時不建立 `id`、`type`、`status`、`raw_path`、`maps` 或 `related_notes`；這些正式治理欄位要等 Assess／Register 後才能可靠填入。

在 Web Clipper Settings 將 `TYT-KM` 加到 Vaults，再匯入模板並視需要設為 fallback。Highlighter 建議保留頁面脈絡；只剪節錄時，後續 read scope 必須標 partial。Interpreter 預設關閉，以避免沒有收益的延遲、費用與內容外傳。

## 從剪藏到來源

剪藏後可先 Assess。只有 Register Trigger 成立並取得授權時才：

1. 指派 source ID。
2. 把剪藏移到 `10_Sources/{YEAR}` 並改名；此後視為原件。
3. 將影響理解的圖片保存到可追溯位置並更新連結。
4. 先讀文字，再查看重要圖像。
5. 建立 Source Note 並完成 Register／Ingest Verify。
6. Integrate Trigger 另由 Router 判斷。

Web Clipper 預設可能只保留遠端圖片 URL；Inbox 附件只是暫存，Register 後應和來源維持可追溯關係。
