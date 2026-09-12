---
id: SYS-REF-AUTHORING-STRUCTURE
type: system-guide
status: active
created: 2026-09-10
updated: 2026-09-11
aliases:
  - 筆記寫作與結構指南
---

# Authoring and Structure Guidance

本頁提供非強制的寫作建議與例子，不新增或覆寫正式規則。需要建立或重構筆記時按需載入；正式契約以 [[90_System/Metadata Schema]] 和命中的 Workflow Spec 為準。

## Knowledge Note 寫作

必要段落、canonical 位置與推論標示依 [[90_System/Metadata Schema#Knowledge Note 正文方法]]。建議依模板順序展開，Evidence 按主張組織，方便比較不同來源如何支持或限制同一結論。

例如，解釋某個通用方法時，可連到 Source Note 的數值證據及 Project 的應用情境，讓讀者按需追查細節。

## Source Note 寫作

正文與 claim card 契約見 [[90_System/Metadata Schema#Source Note 正文方法]]。建議依來源自身的問題、方法、結論與限制組織，讓每張 claim card 聚焦一個可引用主張。

## 連結與關係

- Wikilink 可用 alias 改善句子；embed 用來呈現同一內容，不建立第二份真相。
- 更新核心頁前查看 backlinks，判斷下游同步；backlink 只表示被提及，不自動表示支持。
- 正文用自然語言說明 depends on、explains、contrasts with、qualifies、contradicts、applies to 或 derived from；避免只有「Related」的裸連結。

## 拆分與合併

考慮拆分：一頁回答多個可獨立演進問題；各部分來源、status 或更新頻率不同；Index 無法用一行準確描述。

考慮合併：頁面沒有獨立結論；只因同義詞或來源不同而重複；內容總是一起讀且導航比正文更多。

## 完稿自查

- 標題與 aliases 可搜尋，一句話能說明所回答的問題。
- 事實、來源主張、推論、觀察與決策已分開。
- 外部主張有 Source Note 與 locator；限制與衝突未省略。
- 有至少一個有語意的入口，或說明暫時孤立理由。
- 空模板段落已刪除；Index、Map、Context 與日誌按需同步。
