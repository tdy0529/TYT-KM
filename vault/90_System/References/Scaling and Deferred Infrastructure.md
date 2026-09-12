---
id: SYS-REF-SCALING-DEFERRED
type: system-guide
status: active
created: 2026-09-10
updated: 2026-09-10
aliases:
  - 規模策略與延後工具
---

# Scaling and Deferred Infrastructure

本頁是按需參考，不屬日常載入路徑。增加工具的 Trigger 是可觀察的搜尋、維護或一致性問題，不是頁數本身。

## 小型（約少於 100 正式頁）

使用 Knowledge Index、Maps、Search、Wikilinks 與局部 lint。一次處理少量來源；不先建立向量資料庫、Dataview 或自動化。

## 中型（約 100–1,000 正式頁）

用 Knowledge Catalog.base 管理狀態，增加高品質 Maps，批次完整 lint。只有已知內容的召回失敗成為瓶頸時，才評估本機全文或混合搜尋。

## 大型（超過約 1,000 正式頁或大量多媒體）

可分片 Knowledge Index，增加可重現 validator、來源雜湊與 migration；依實測評估全文／向量搜尋。多人協作再加入角色與 review queue。

## 刻意延後

- 不以學科建立頂層資料夾。
- 不預建空 Map 或 Project。
- 不保存每段聊天。
- 不要求所有材料先完整 Ingest。
- 不先依賴雲端向量庫、Dataview 或更多外掛。
- 不把 Canvas 或 graph 當作唯一知識載體。

若要啟用其中一項，先記錄目前失敗案例、預期改善、維護成本、驗證方法與 rollback。
