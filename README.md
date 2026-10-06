# 感謝日記（第一版）

全家一起寫感恩日記的 PWA 網頁。單檔 `index.html` + Firebase Firestore + GitHub Pages。

## 檔案
| 檔案 | 用途 |
|---|---|
| `index.html` | 整個 App（畫面、邏輯、匯出圖片都在裡面） |
| `manifest.webmanifest` | 讓它可以安裝到手機桌面 |
| `sw.js` | 讓頁面離線也能開、更新時自動拿最新版 |
| `icons/` | App 圖示（180 / 192 / 512 / 可遮罩 512） |

## 上線步驟（GitHub Pages）
1. 在 GitHub 網站新建 repo（例如 `Gratitude`），把**整包檔案**（含 `icons` 資料夾）用「Add file → Upload files」拖進去。
2. Settings → Pages → Branch 選 `main`、資料夾 `/ (root)`，儲存。
3. 網址會是 `https://wangchiapin.github.io/Gratitude/`。

## 連上 Firebase（已設定好）
`index.html` 裡的 `FIREBASE_CONFIG` 已填入專案 `gratitude-wall-ef60d`。還需要在 Firebase 控制台做兩件事：
1. **建立資料庫**：Build → Firestore Database → 建立資料庫（位置建議 `asia-east1` 台灣；模式選「正式版」即可，規則下一步會換掉）。
2. **貼上規則**：Firestore Database → 規則（Rules）→ 把 `firestore.rules` 的**全部內容**貼上取代 → 發布。

資料存在這幾個 collection：`gratitude_members`、`gratitude_posts`、`gratitude_likes`、`gratitude_ledger`、`gratitude_settings`。

> 這個 App 沒有帳號系統，規則分不出「是誰」在操作，所以管理密碼和幣的規則是擋家人誤按，不是防駭客，家用夠用。`gratitude_ledger` 只允許新增不允許覆寫，所以同一筆幣（例如同一天的登入）不會被重複領。管理密碼預設 `0000`，上線後請先到「更多 → 設定」改掉。

## 家人怎麼安裝
- 在 LINE 貼網址 → 點開後，右下角「⋯」→「用預設瀏覽器開啟」（iPhone 用 Safari、Android 用 Chrome）。
- iPhone：分享 ⬆️ →「加入主畫面」。Android：選單「⋮」→「安裝應用程式」。
- App 裡的「更多 → 安裝到手機桌面」也有同樣的圖文教學。

## 功能與規則
- 角色：爸爸、媽媽、爺爺、奶奶、哥哥、姊姊、弟弟、妹妹（管理員可增減），每人自選暱稱和動物頭像，裝置會記住。
- 一天一篇，每篇 1～3 條（每條最多 80 字），可選「想謝謝誰」，也能自己新增其他感謝對象（例如王阿姨），名字會記在自己的名單裡；自己的日記可修改、刪除，管理員可刪任何一篇。
- 感恩幣：每日登入 +1、寫日記 +3、按讚別人 +1（被按讚的人也 +1，不能讚自己、每篇一人一次、每人每天最多 5 次有幣）。
- 刪除日記會收回那篇產生的所有幣與愛心；之後可以重寫並重新領 +3。
- 日期一律用台灣時間（UTC+8）。
- 兌換區：目前只有「獎勵準備中」畫面。
- 月回顧與匯出：回顧圖、整月日記（自動分成多張 JPG）、單篇日記圖。

## 尚未做（之後可加）
獎勵清單與兌換流程、每晚推播、照片、LINE 機器人 / LIFF 自動登入。
