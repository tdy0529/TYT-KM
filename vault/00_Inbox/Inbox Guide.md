---
id: SYS-GUIDE-INBOX
type: system-guide
status: reviewed
created: 2026-09-03
updated: 2026-09-10
aliases:
  - 收件匣說明
---

# Inbox Guide

00_Inbox 是最低摩擦的暫存入口，不是永久分類，也不是可靠知識來源。

## 可以放進來的內容

- 尚未判斷價值的文章、PDF、圖片、錄音與剪藏
- 臨時想法、問題、待整理筆記
- Obsidian 自動接收的新筆記
- 尚未知道屬於來源、知識或專案的材料

附件預設進入 00_Inbox/_attachments。

Web Clipper 的通用模板會把網頁存到 `00_Inbox/Web Clips`。這些檔案是未登記的來源候選：可供 LLM 執行 Assess，但在取得 source ID 並完成 Register 前，不得當成正式證據或可靠知識引用。

## 不應長期留在這裡

- 已被專案使用、需要穩定引用的材料
- 已形成可重用理解的內容
- 已確認的專案決策與交付物

## 清理時的四種去向

1. 無價值：經確認後刪除。
2. 只屬於某專案：移至該專案的 Worklogs、Outputs 或專案附件區。
3. 值得保留的外部材料：依 [[90_System/Workflow Specs/Register and Ingest]] 處理。
4. 已能形成通用理解：建立或更新 20_Knowledge 的筆記，並補上依據。

本頁是系統錨點，不參與 Inbox 清理。

最短處理語句：

- 「Assess 這篇剪藏是否值得讀，以及是否適合目前專案。」
- 「把這篇剪藏 Register、Ingest，並整合真正有用的主張。」
- 「這篇只服務目前專案，移入專案 Worklog，不要升級成長期知識。」
