# 換模型還是加 Effort？拆解 Claude Code 那顆最常被轉錯的旋鈕

![換模型還是加 Effort？](images/summary-banner.webp)

本專案是把 Anthropic 官方文章 **《Choosing a Claude model and effort level in Claude Code》** 消化、重新整理成的白話深度導讀，並記錄了整個人機協作產出這份導讀的完整過程。專案本身即是「人機協同開發」的一個實例。

---

## 🔗 參考來源

- **原文網址**：[Anthropic Blog — Choosing a Claude model and effort level in Claude Code](https://claude.com/blog/claude-model-and-effort-level-in-claude-code)
- **原作者**：Lydia Hallie，Anthropic Claude Code 團隊
- **發布日期**：2026 年 7 月 7 日

本專案的導讀文字並非原文翻譯，而是消化原文核心概念後，用白話、台灣用語重新撰寫的原創內容；文中部分插圖直接引用原文圖表（供讀者對照原文），另一部分是依段落內容另外生成的原創 kawaii 風格資訊圖。

---

## 📂 檔案結構

| 檔案 / 目錄 | 說明 |
|---|---|
| `index.html` | 正式上架的導讀網頁（GitHub Pages 首頁），含摘要、五段主敘事、模型角色速查表、開發者工具箱、總結 |
| `deep_guide.md` | `index.html` 對應的 Markdown 原始稿，適合在 Obsidian / Typora 離線閱讀 |
| `deep_guide.normalized.md` | 經過中文標點正規化的版本（供轉檔流程使用） |
| `images/` | 文章插圖，統一為 `.webp` 格式（壓縮率高、體積小）。分兩類：`tokenization.webp`／`frozen-weights.webp`／`effort-comparison.webp`／`output-tokens.webp`／`decision-framework.webp`／`routine-tokens.webp`／`complex-tokens.webp` 是原文插圖；`infographic-*.webp` 是另外生成的原創 kawaii 資訊圖 |
| `claude_model_effort_level_guide.md` | 專案早期版本的導讀摘要（五幕結構，融合多重思維濾鏡），保留作為歷史版本參照 |
| `legacy-index.html` | 專案最早期的 Notion 風格導讀網頁草稿，尚未正式發布過，保留作為歷史版本參照 |

---

## 🧭 這份導讀在說什麼

一句話版本：**模型決定 Claude「懂不懂」，是能力天花板；Effort 決定它「願不願意做確實」，是天花板底下走多遠。** Claude 給錯答案時，應該先確認資訊給齊了沒，再判斷它是「真的不懂」還是「懂但沒做確實」——不懂換模型，沒做確實加 Effort，兩者的解法不能對調。從花費來看，例行工作留給便宜模型、用預設 Effort 最划算；真正複雜模糊的任務，一開始就上貴模型、開高 Effort，總花費反而更低。

---

## 🤝 完整互動過程（從頭到尾）

這份導讀不是一次寫成的，而是在一連串來回對話中逐步修正出來的。以下依實際發生順序記錄，方便回顧當初每個決定的脈絡：

### 1. 起點：讀懂舊專案的方法論
對話一開始，先讀了本目錄既有的 `README.md`，了解這是一個把 Anthropic 部落格文章內化成實作流程的專案，核心方法論是「實作前盲點檢視 → 實作中偏差記錄 → 實作後隨堂測驗」的三階段人機對齊迴路，並確認了當時已存在 `index.html`（Notion 風格導讀）與 `claude_model_effort_level_guide.md`（精簡摘要指南）兩份產出。

### 2. 正式任務：用三個 skill 重做一份導讀
使用者接著提出正式需求：用 `ai-mentor-agents`、`deep-guide`、`md_to_html` 三個 skill，針對原文 URL 做一次新的導讀，圖片可以引用原文，行為指引參考同目錄下另一個專案 `claude_fable_unknowns_guide` 的做法（該專案示範了「單一敘事、不暴露寫作框架、圖片嵌入搭配燈箱、白話化改寫給零基礎讀者」的產出風格）。

依此展開了以下步驟：
1. 讀取 `claude_fable_unknowns_guide/README.md`，確認其記錄的方法論與踩坑經驗（例如「兩篇拼接」問題、術語太難、Mermaid 語法錯誤等前車之鑑）。
2. 用 WebFetch 取得原文的概念摘要與圖片清單（未逐句轉錄全文，只取核心概念與圖片 URL，避免逐字複製原文）。
3. 下載原文的 8 張核心插圖到 `images/`（斷詞示意圖、唯讀權重圖、Effort 對比圖、輸出分類圖、診斷決策圖、簡單／複雜任務的花費曲線圖），1 張連結失效的圖片捨棄不用。
4. 逐張檢視圖片內容，確保後續文字描述與圖片實際內容一致。
5. 撰寫原創的五幕式深度導讀（不逐句翻譯原文，而是消化後用自己的話重新組織論證），融合白話比喻與工程視角。
6. 建立 `effort_deep_guide.html`（後改名為 `index.html`），套用 Notion 風格排版、sticky 導覽列、深色模式、圖片點擊燈箱效果，並用 `html.parser` 驗證語法、Playwright 做桌機／手機截圖 QA。
7. 發布到 Artifact 供使用者線上預覽。

### 3. 使用者要求：存到本地，不要雲端
使用者澄清需求的是本地檔案而非雲端連結。說明本地檔案本來就已經存在，Artifact 只是額外的雲端預覽管道，並用 Finder 打開檔案所在目錄供確認。

### 4. 白話化改寫
使用者回饋「要白話易懂」。逐段檢視原本較生硬的技術用詞（例如「斷詞」「唯讀權重」「Steering / Teaching」「併發問題」），改寫成生活化比喻（例如把模型權重比喻成「一顆寫死的大腦」），同步修改 `deep_guide.md` 與 `index.html`（當時檔名還是 `effort_deep_guide.html`），並重新驗證語法與截圖。

### 5. 兩岸用語檢查
使用者要求「用台灣人通用的語氣與名詞，不要採中國的用字」。逐句掃描全文比對常見兩岸用語差異（檔案 vs 文件、程式碼 vs 代碼、記憶體 vs 內存、品質 vs 質量等），確認全文本來就已使用台灣慣用字，無需修改。

### 6. 「心力」不是台灣人熟悉的說法
使用者指出「心力」這個譯詞聽起來陌生。依照全域 CLAUDE.md 的規則「技術術語與程式碼識別符保持英文原文」，把全文的「心力」全部改回 Claude Code 介面上實際使用的英文設定名稱 **Effort**，讓讀者對照 Claude Code 介面時能直接對得上。

### 7. 加摘要、總結，並補生圖 Prompt
使用者要求：（1）文章開頭加摘要、結尾加總結；（2）檢視適合的段落，整理對應的資訊圖表生圖 Prompt（台灣用語繁體中文、粉圓體、日系 kawaii 風格、16:9）。
執行內容：
- 在文章開頭加了摘要區塊（highlight box），文末加了「總結」段落，收斂成 5 條重點清單。
- 針對「模型 vs Effort 比喻」「判斷分岔」「花費效益對比」三個段落，分別撰寫 kawaii 風格生圖 Prompt，用 `codex exec` 的 `image_gen` 工具實際生成 3 張原創插圖（`infographic-model-effort.png`、`infographic-diagnose.png`、`infographic-economics.png`），嵌入對應段落並套用既有的燈箱效果。

### 8. 準備上架：檔名衝突與 GitHub Pages
使用者要求：（1）把工作用的 HTML 檔改名為 `index.html`；（2）把完整互動過程寫進本檔案；（3）上架到 GitHub Pages，帳號 `lishinshang`，repo 名稱 `claude-model-tuning`。

執行過程中發現目錄裡已經有一份更早期的 `index.html`（就是第 1 步提到的、當時還沒發布過的 Notion 風格草稿），與新檔案改名會直接衝突。詢問使用者如何處理後，使用者選擇「合併好用的部分進來」。因此：
- 從舊版 `index.html` 中挑出仍然有價值、新版導讀沒有涵蓋到的內容——**模型角色速查表**（把 Fable / Opus / Sonnet 類比成專科專家／專家／優秀通才）與**開發者工具箱**（盲點檢視、偏差記錄、隨堂測驗三個可一鍵複製的協作提示詞）——重新整理措辭後加進新版導讀，補上對應的表格與複製按鈕樣式。
- 把舊版 `index.html` 改名為 `legacy-index.html` 保留下來，把工作檔正式改名為 `index.html`。
- 重新驗證 HTML 語法、確認所有圖片路徑在改名後依然正確載入。
- 撰寫這份完整歷程記錄（也就是你現在讀到的這份 `README.md`）。
- 初始化 git、建立 GitHub repo `lishinshang/claude-model-tuning` 並推送、啟用 GitHub Pages。過程中確認 gh CLI 實際登入的帳號拼法是 `lushinshang`（跟使用者原本說的 `lishinshang` 不同），先跟使用者確認後才建立 repo。

### 9. 全文總覽圖、統一圖片格式
使用者接著要求：（1）用同樣的 kawaii 風格生成一張涵蓋全文重點的橫幅圖，放在文章開頭，讓 GitHub 也能直接看到預覽圖；（2）所有圖片轉成 `.webp`；（3）更新這份 README 並上傳。

執行過程：
- 用 `codex exec` 的 `image_gen` 生成橫幅圖，但因為卡片數量多、prompt 較長，連續三次嘗試都在時限內沒完成（timeout），簡化 prompt 重試也還是超時。使用者主動決定先跳過這一項，改成在本檔案留 TODO，之後再繼續生成。
- 用 `cwebp` 把 `images/` 內所有原文插圖與原創 kawaii 插圖（共 10 張）轉成 `.webp`，品質設定 85，檔案體積平均縮小到原本的 15-20%；同步更新 `index.html`、`deep_guide.md`、`deep_guide.normalized.md`、本檔案裡所有的圖片路徑，刪除轉檔後不再使用的原始 `.png`／`.svg` 檔案。
- 更新這份 README（新增本節與待辦區塊），commit 並推送到 GitHub。

### 10. 全文總覽 banner 圖：找出逾時的真正原因
使用者回頭要求繼續補上第 9 步擱置的橫幅圖。連續幾次調整 prompt（減少卡片數、簡化描述、拉長 timeout）都還是在腳本層級 timeout，於是換個角度先驗證問題出在哪：直接用一個完全不含中文、極簡單的 prompt（紅色圓形）呼叫 `codex exec`，結果幾秒內就成功——證明 `image_gen` 工具本身沒問題。接著直接（不透過 `codex_imagegen.py` 這層包裝腳本）用單一機器人角色 + 中文標題的 prompt 呼叫 `codex exec`，同樣很快就成功產出圖片。判斷問題出在包裝腳本的驗證／重試邏輯，而非圖片產生本身，因此改為繞過包裝腳本、直接呼叫 `codex exec` 生成，再手動搬移、轉檔、嵌入頁面與 README。

---

## 💡 過程中學到的事

- **原文轉譯不是逐字翻譯**：用 WebFetch 取摘要而非全文轉錄，逼自己用自己的話重新組織論證，反而讓文章更適合白話化改寫。
- **術語要對照實際介面**：把「心力」改回「Effort」的教訓是——當一個詞是產品介面上的實際設定名稱時，硬翻成中文反而製造理解落差，這時候應該保留英文原文。
- **舊檔案不是理所當然可以覆蓋的**：改檔名撞到既有檔案時，先問使用者要怎麼處理，比自己猜測「反正舊的比較不重要」更安全；使用者的答案（合併有用的部分）也確實比單純二選一（留舊 / 蓋掉）更好。
