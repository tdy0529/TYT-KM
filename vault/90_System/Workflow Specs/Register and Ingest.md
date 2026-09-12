---
id: SYS-WF-REGISTER-INGEST
type: system-doc
status: reviewed
created: 2026-09-10
updated: 2026-09-10
aliases:
  - Register Workflow
  - Ingest Workflow
---

# Register／Ingest

## Trigger

- 來源將被可指名的專案決策引用，且能說明所支持的主張。
- 已辨識可定位、可重用的具體證據及其知識缺口或用途。
- 網頁可能變動，需要穩定快照。
- 使用者明確要求加入知識庫。
- 已登記來源的 Source Note 缺少經原件核對後、下次仍會需要的 source-specific claim、推導、術語、條件或限制。

候選評估或「未來可能有用」本身不足以成立 Trigger。

## Read

讀來源、現有 Assess handoff、相鄰 Source Notes，以及判斷重複或連結所需的 Index／Maps／Notes。長文件依 [[AGENTS]] 控制範圍。

## Register

新來源才執行本段；更新既有 Source Note 時沿用原 source ID 與原件。

1. 指派下一個未使用的 `SRC-YYYY-NNNN`。
2. 原件放入 `10_Sources/{YEAR}/` 並以前綴命名；既在 Inbox 時移動而不保留副本。
3. 只有 URL 時記錄 accessed；重要或不穩定內容優先保存合法快照。快照的 raw_path 與原 URL 都要保留，Read scope 說明實際所讀版本。
4. 不改寫原件；OCR、轉錄或清理結果另存並記錄關係。
5. 建立同 ID 的 Source Note。

## Ingest

1. 有 Assess handoff 時先核對授權與落點；claim 回原件確認 locator，推論與 user judgment 保留角色，reusable synthesis 不在 Source Note 展開成通用結論。
2. 判斷來源問題、範圍、方法、結論與限制；含圖材料先讀文字，再逐一查看影響理解的圖像。
3. 以 claim 為單位記錄關鍵內容，每個重要 claim 附 locator。
4. 分開來源結論、LLM 推論、使用者判斷、未證實處與內部矛盾。
5. 記錄實際 read scope；partial 不得寫成完整處理。
6. status 依範圍使用 registered、partial 或 processed。

## Write

- 原件：`10_Sources/{YEAR}/SRC-...`。
- 解讀：建立或更新 `20_Knowledge/Source Notes/SRC-... - {TITLE}.md`。
- 更新 [[20_Knowledge/Knowledge Index]] 的 Source Notes，並依執行契約記錄 ingest。
- 若出現跨情境理解，只交回 Router 判斷 Integrate；只要求穩定登記時停止。

## Verify

- source ID 唯一，原件或 URL 可開啟。
- Source Note 有來源資訊、read scope、claims、locator、限制與關聯，status 符合實際範圍。
- Index 與日誌已更新。
- handoff 中應由 Source Note 承載且已授權的成果已寫入或明列未保存；user judgment 沒有被寫成來源主張。

## Approval

使用者已要求保存來源，或登記是完成已授權交付物所必需時，可直接執行。若目前只要求理解、候選判斷或最小專案進度，先提出具體證據、用途與預計位置。來源授權不明、含敏感資料、需外部存取或將覆蓋原件時先確認；既有清楚授權不重複詢問。
