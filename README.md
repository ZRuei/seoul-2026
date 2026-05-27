# SHINee 首爾行 2026 — 互動行程網站

單檔靜態 HTML，行動裝置優先。

## 本機預覽（30 秒測試）

直接雙擊 `index.html` 在瀏覽器打開即可。或在這個資料夾跑：

```bash
python3 -m http.server 8000
```

然後手機/電腦瀏覽 `http://localhost:8000`。

---

## 部署到 GitHub Pages（10 分鐘上線）

### 1. 建 GitHub repo

- 到 https://github.com/new
- Repository name：`seoul-2026`（隨意，但會出現在網址裡）
- Public（GitHub Pages 免費版需要 Public，私人行程資料**不要寫死在 index.html**，請放雲端 Gist 同步）
- **不要**勾 Initialize with README（避免衝突）
- Create repository

### 2. 推這資料夾上去

```bash
cd /Users/ruei/Desktop/project/SHINEE-adventure/seoul-2026
git init
git add index.html README.md
git commit -m "Initial: SHINee 首爾行 2026 行程網站"
git branch -M main
git remote add origin https://github.com/<你的帳號>/seoul-2026.git
git push -u origin main
```

### 3. 啟用 Pages

- 回 repo 頁面 → Settings → Pages
- Source 選 `Deploy from a branch`
- Branch 選 `main` + `/ (root)` → Save
- 等 1–2 分鐘，網址會出現：`https://<你的帳號>.github.io/seoul-2026/`

### 4. 手機加入主畫面

- iOS Safari 打開網址 → 分享按鈕 → 「加入主畫面」
- Android Chrome → 選單 → 「新增到主畫面」
- 之後點圖示就像 App 一樣全螢幕

---

## 設定雲端同步（GitHub Gist）

讓三人在不同手機看到的順序/備註是同一份。

### 1. 產 Personal Access Token

- 到 https://github.com/settings/tokens
- 點 **Generate new token** → **Generate new token (classic)**
- Note 填：`seoul-2026-gist`
- Expiration 選 90 days（建議；旅程結束後過期）
- Scopes **只勾 `gist`**（其他都不要勾，這是只能讀寫 Gist 的最小權限）
- 拉到底 Generate token
- **複製出來的 `ghp_xxxxxxxx`**（離開頁面就看不到了！）

### 2. 在網站建立 Gist

- 打開部署好的網站 → 右上 ⚙️ 設定
- Token 欄貼上剛複製的 `ghp_xxxxxxxx`
- 按 **建立新 Gist**
- 成功後會自動填入 Gist ID
- 之後每次改動會自動同步到雲端

### 3. 第二、三隻手機同步

- 在第一隻手機的設定 → 看到 Gist ID
- 另一隻手機打開網站 → ⚙️ 設定
- 貼上**同一個 Token + Gist ID**
- 按 **拉取雲端** → 抓到一樣的資料

> **安全提醒**：Token 等於小型密碼，**只貼在自己信任的手機**。三人共用同一個 Token 是 OK 的，但旅程結束後到 GitHub 把它 Revoke 掉。

---

## 功能速覽

底部 3 個分頁：🗓 行程 / 🎒 行李 / 🗺 地圖。

### 🗓 行程
| 操作 | 怎麼做 |
|---|---|
| 切換日期 | 點頂部日期 tab |
| 看當日天氣 | 進日期時自動顯示溫度、文字、降雨機率（>=60% 顯示 BRING UMBRELLA tag）；點卡片可手動 refresh；下方有 KMA / NAVER 外連 |
| 勾選完成 | 點時間旁的方框 |
| 拖曳排序 | 長按左側 `⋮⋮` 拖動 |
| 加備註 | 卡片底部「📝 加備註」 |
| 編輯時間/名稱 | 卡片右上 `⋯` → 編輯 |
| 隱藏（不去） | 卡片右上 `⋯` → 隱藏 |
| 新增點位 | 每日底部「＋ 新增備案點位」 |
| 打開 Naver Map | 卡片底部「📍 Naver Map」 |
| 搜尋（跨日） | 右上 🔍，可搜店名/備註 |

### 🎒 行李清單
- 8 個分類（出發前數位 / 證件現金 / 行動電子 / 演唱會 / 衣物 / 盥洗藥品 / 採買 / 託運）
- 共 50 項預設項目；可勾選、可新增、可刪除自訂項目
- 三人**共用同一份**（透過 Gist 同步）
- 分類頭可摺疊（點分類名）
- 頂部顯示總進度

### 🗺 地圖
- Leaflet + OpenStreetMap（免費、無 API key）
- 上方日期 chip 可切換「全部 / 單日」
- 每日點位用不同顏色標示
- 點 pin 跳出資訊 → 可直接連到 Naver Map 該店
- 飯店永遠顯示
- 不需要登入

### ⚙️ 設定
| 項目 | 用途 |
|---|---|
| 雲端同步 | 設 Gist token / 建立新 Gist / 拉取雲端 |
| 顯示已隱藏項目 | 找回隱藏掉的點 |
| 匯出 / 匯入 JSON | 本機備份 |
| 重置 | 清空勾選/備註/排序回到原始計畫 |

---

## 常見問題

**Q: 沒有 GitHub 帳號也能用嗎？**
A: 可以，所有資料會存在手機瀏覽器 localStorage。缺點是**換手機/清快取會遺失**註記，且三人之間不同步。

**Q: 同步失敗（紅色「同步失敗」）？**
A: 通常是 Token 過期或 Gist ID 錯。⚙️ 重新貼一次。

**Q: 想離線用？**
A: 第一次打開後資料會存本機，**沒網路也能讀**（只是無法同步到 Gist）。在地鐵裡可以放心看。

**Q: 怎麼改預設行程？**
A: 改 `index.html` 裡 `DEFAULT_DATA` 物件 → 重新 `git push` → Pages 1 分鐘後更新。

**Q: 一筆 Naver Map 連結點下去找不到？**
A: 編輯該項目 → Naver 搜尋詞改成韓文店名（中文常找不到，韓文最準）。

---

## 結構

```
seoul-2026/
├── index.html      # 全部（HTML/CSS/JS/資料）都在這
└── README.md       # 這份說明
```

CDN 依賴：SortableJS（拖曳排序）— 第一次載入後瀏覽器會 cache。

---

## 設計風格

Editorial / gallery 美學：純白底、無陰影、無圓角、極細灰線分隔、Inter + Noto Sans TC 字體、湖水綠 accent 極度節制使用（僅 hover / active）。Icon 使用 Lucide inline SVG（無 emoji）。

### 資訊階級
- **ANCHOR**（左邊綠線 + Black 900）：時間固定、有預約、演唱會
- **OPTIONAL**（50% 透明 + Light 300）：「如尚開放 / 視體力 / 視當天」自動偵測
- **DEFAULT**（Bold 700）：一般行程
- **DONE**（刪除線）：勾選完成
