---
id: SYS-003
type: system-decision
status: accepted
created: 2026-09-10
updated: 2026-09-10
aliases:
  - 未登記材料後續追問路由決策
affects:
  - "[[90_System/Workflows]]"
---

# SYS-003 — Clarify Assess and Query Boundary

## Context

流程二以材料位置區分 Assess 與 Query：未登記外部材料一律走 Assess；流程五 Trigger 卻允許「已由先前 Assess 處理過」的材料進入 Query。實際使用時，同一份未登記文章的後續追問仍可能主要依賴原文，寬鬆解讀會讓暫時的對話脈絡被誤認為庫內證據，也使 Query 的「Wiki 沒有答案時停止並重路由 Assess」無法一致執行。

使用者於 2026-09-10 根據實際文章理解流程指出此矛盾，並明確要求直接修改核心規則。

## Decision

同一份未登記外部材料的後續追問，只要答案仍主要依賴該材料，就維持或重新進入 Assess。先前完成 Assess 只表示已評估當時的讀取範圍，不會把材料轉成庫內內容或持久的 Query 證據。

採用「移除材料測試」判斷路由：暫時移除未登記材料後，若 Wiki 仍足以回答目前問題，走 Query；若不足，走 Assess；若同時需要外部材料與 Wiki 綜合，先完成 Assess 的 Verify，再重路由至 Query，不巢狀執行。

## Rationale

- 保持「材料位置決定 Assess／Query」的一致邊界。
- 區分當前對話可繼續分析的暫時脈絡，以及可由 Vault 穩定找回的持久證據。
- 防止 Query 在 Wiki 無答案時直接依賴未登記材料，繞過 Assess 的 read scope、來源／推論分離與評估要求。
- 「移除材料測試」提供可操作的判準，不依賴「主要依賴」的直覺判斷。

## Alternatives

### Assess 一次後，所有後續追問都進 Query

未採用。這會把完成一次評估誤當成來源已入庫，且未解決跨會話找回與來源定位問題。

### 未 Register 前禁止任何後續分析

未採用。Assess 的目的就是讓使用者不必先完整入庫，也能理解材料並決定是否繼續投入。

### 每個混合問題在同一 workflow 內同時處理

未採用。這會破壞 Router Contract 要求的 block 分離、Verify 與重路由順序。

## Consequences

- 未登記材料可以在當前工作鏈持續接受追問，但相關回答仍屬 Assess，不能被表述為持久的 Wiki 證據。
- Query 可使用由 Assess 引出的問題，但前提是拿掉未登記材料後，Wiki 本身仍足以回答。
- 同時需要文章內容與既有 Wiki 的問題，會先完成 Assess，再以已標示的理解重路由 Query 做綜合。
- 若希望未來不重新讀取附件即可查詢，仍需 Register／Ingest；若要成為跨情境知識，再依 Trigger Integrate。

## Migration

- 更新 Workflows 的 Assess Trigger，加入未登記材料後續追問與移除材料測試。
- 更新 Query Trigger，移除「只因先前 Assess 過即可進 Query」的寬鬆條件。
- 不修改既有 Source、Knowledge、Project 或歷史日誌；歷史執行結果不回溯重分類。

## Rollback

- 移除 Assess Trigger 新增的後續追問段落。
- 把 Query Trigger 還原為允許「已由先前 Assess 處理過」的原句。
- 移除 Query Trigger 後的持久證據說明；不影響任何既有來源或知識頁。

## Revisit when

- 實際問題無法用移除材料測試穩定分類。
- 同一材料的多輪 Assess 造成不必要的重複輸出或讀取。
- 系統新增明確的 session-scoped evidence type，能安全承載未登記但已評估的材料。
