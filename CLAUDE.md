# CLAUDE.md — 星塵夢汐 Stardust DreamTide

Non-negotiable rules for every Claude session working in this repository.
不用先問就能做的事：§7 自主權矩陣。文件與舊檔放哪裡：§8。不捏造、不悄悄替換：§9。
全網路背景（Blue 是誰、agent 名冊、8 個 repo 地圖、跨 repo 規則）只在
`Blue_Astral_Nexus_Engine/AGENT_STATUS.md` §1–3；本 repo 的現況在 `AGENT_STATUS.md`。

## 0. 這個 repo 是什麼

`stardust.bluechiou.com`：情緒紀錄、日記、夢境、水晶圖鑑的 PWA。靜態 vanilla JS（沒有 build 框架）
＋ Vercel serverless（`api/`）。不屬於 ÆTHNOUS 品牌，但擁有者相同，全網路鐵律一樣適用。

## 1. 使用者資料永不外流（鐵律）

- 使用者的情緒、日記、夢境、許願、健康資料，敏感程度**至少等同生辰**。不得進 git、log、
  文件、PR、截圖。測試資料一律用假資料。
- 星塵帳號是端對端加密：伺服器只存密文和 verifier，看不到密碼、金鑰或明文
  （`docs/account-setup.md`）。任何會讓後端讀到明文的改動都算 🔴。
- 健康資料（例如生理期）另有更嚴格的界線：`docs/cycle-moon-vision.md` 第零節。

## 2. Secrets

永不 hardcode。只放在 Vercel 環境變數：`ANTHROPIC_API_KEY`、`NOTION_TOKEN`、`STARDUST_AI_MODEL`、
`STARDUST_GOOGLE_CLIENT_ID`、`ACCOUNT_KV_URL`／`ACCOUNT_KV_TOKEN`、`BOARD_KV_URL`／`BOARD_KV_TOKEN`
（完整清單以 `README.md`「部署」為準）。

## 3. 架構速查

```
index.html / app.js / style.css   單頁 App（APP_VERSION 在 app.js）
crystals.js                       水晶圖鑑・收藏架・月相許願（docs/crystal-vision.md）
account.js + api/account.js       星塵帳號（E2E 加密同步，Upstash Redis）
cloud.js                          Google Drive 備份
sw.js                             Service Worker（網路優先；CACHE 字串）
api/                              ai-chat（夢汐）· notion-sync · board · feedback · referral · register · space-news · config
```

## 4. Workflow

- Surgical changes only；成功標準先寫再動工。
- 錯誤回應一律用通用訊息（不外洩 stack）；所有渲染到 HTML 的使用者輸入都要先 escape。
- 發新版：`app.js` 的 `APP_VERSION` 和 `sw.js` 的 `CACHE` 要**一起**往上加（`README.md`「改版之後」）。
- Vercel 後台**不要**對舊的 deployment 按 Redeploy，那等於回滾 production（2026-07-28 事故）。

## 5. 禁止擅自排程（鐵律）

除非 Blue 明確下指令「請安排 Auto check」，不得建立任何 send_later、trigger、routine、
scheduled check-in 或推播。自 2026-07-29 起由 `.claude/settings.json` 的 `deny` 在工具層擋掉，
2026-08-04 擴大清單（起因：2026-07-29 一個自我續命的 PR 監看迴圈，一夜燒掉約 12% 的週用量）。**不要為了
「只看一次」或「只通知一次」而移除任何一條 deny。** PR 需要追蹤時，用 `subscribe_pr_activity`
（事件驅動）。

## 6. 時間與日期判定協議（鐵律）

絕不用 WebSearch／WebFetch 確認「今天日期」。只能用程式碼＋明確的 IANA 時區計算。
使用者端的時區用前端 `Intl.DateTimeFormat().resolvedOptions().timeZone`，不要用 IP 推斷。
月相、連續紀錄等日期邏輯用日期元件推算，不用毫秒相減（日光節約時間）。
完整協議見 `Blue_Astral_Nexus_Engine/CLAUDE.md` §8。

## 7. 自主權矩陣（Blue 2026-09-25 核准）

預設是**直接做**，只有 🔴 需要先問 Blue。Blue 在 session 裡當場下的指令本身就是核准。

| 等級 | 範圍 | 例子 |
|---|---|---|
| 🟢 直接做 | 可逆、只在分支上、不碰 production | 讀碼、開分支、commit、push 到自己的分支、開 **draft PR**、寫／修文件、更新過期的 `AGENT_STATUS.md` |
| 🟡 做完回報 | 可逆，但別人看得到 | PR 轉 ready、回覆自己 PR 上的 review、封存文件（§8） |
| 🔴 先問 Blue | 不可逆，或影響使用者資料／營收 | merge 進 `main`（＝上線）、改 Vercel 環境變數、動星塵帳號的加密或 KV 資料、新增會收集使用者資料的功能、推播、刪分支或檔案（封存除外）、對外發佈、任何排程 |

規則衝突時的權威順序：Blue 當場指令 → 本檔 → Engine repo 的 `CLAUDE.md`（跨 repo 鐵律）→ `AGENT_STATUS.md`（只供定位）→ 程式碼註解／README。

## 8. 文件分層與封存（Blue 2026-09-25）

- `CLAUDE.md` 規則 · `AGENT_STATUS.md` 現況＋待辦（短）· `README.md` 產品與操作 · `docs/` 現行文件 · `docs/archive/` 封存（唯讀，不照著做事）。
- 全網路的決策只在 Engine repo：`DECISIONS.md`（已核准，只追加）、`INBOX.md`（想法，不動工）。
- 封存＝搬移，不刪除：`git mv` 到 `docs/archive/`，檔頭加一行 `> 封存 YYYY-MM-DD｜原因｜被 <檔名> 取代`。修改過的檔案以 git 歷史為舊版，不另存副本。
- 2026-10-01 起先決策、後施工：新的產品想法先進 `INBOX.md`，寫進 `DECISIONS.md` 才動工。Bug 修正與 Blue 當場指派的工作不受此限。

## 9. No Hallucination Protocol（不捏造、不悄悄替換｜Blue 2026-09-26，Engine `DECISIONS.md` #18）

找不到、不存在、沒驗證的東西，一律明說；不准悄悄換成別的。

- **Agent：** 不把猜測當事實；查得到就自己查，查不到就標「未驗證／待確認」。
- **程式與夢汐：** 讀不到、解不開、同步失敗的紀錄，要明確告訴使用者，不准用空白或舊資料悄悄頂替。
  AI 回覆不得編造使用者沒說過的情緒、夢境或經歷；月相、日期一律由程式算出，不用猜的。
- **審查：** 找到靜默替換＝缺陷；會讓使用者看到錯誤資料的＝S 級。
