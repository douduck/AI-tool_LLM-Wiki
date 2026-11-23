# AGENTS.md — 寵物教學與照護知識庫 (LLM Wiki Schema)

## 1. 專案願景與核心定位 (Project Vision)
本專案為一個由 LLM Agent 全自動維護的**累積型寵物教學知識庫（LLM Wiki）**。
- **核心原則**：原始文獻（`raw/`）為不可變的唯一事實來源（Immutable Source of Truth）；知識庫（`wiki/`）與視覺化教學產出（`slides/`）由 Agent 全權建立、交叉連結與持續維護，確保知識隨新文獻加入而不斷累積與修正，而非每次重新檢索。
- **語氣與風格**：親切、溫暖、具實務指導性的**寵物教學風格**，兼顧科學依據與飼主易讀性。
- **語言規範**：一律使用**繁體中文**撰寫，專業醫學、行為學、營養學或品種專有名詞保留英文（例如：`Separation Anxiety`、`Hip Dysplasia`、`Tear Stains`、`Positive Reinforcement`）。

---

## 2. 目錄結構規範 (Directory Architecture)

```text
/
├── AGENTS.md               # 本規範書（系統運作核心規則）
├── index.md                # 知識庫總目錄（依分類索引所有正式頁面與一句話摘要）
├── log.md                  # 唯讀追加式時間軸日誌（紀錄每次 Ingest / Query / Lint / Verify-Loop）
├── templates/              # 【Agent 參考範本區】存放標準 Markdown 與 HTML 簡報結構範本（不列入 index.md）
│   ├── wiki-page-template.md
│   └── slide-deck-template.html
├── raw/                    # 【唯讀區】存放原始 PDF 教材、文獻、研究報告（嚴禁修改或刪除）
│   └── assets/             # 從原始資料提取或生成的本地圖片資源（如封面水彩插畫）
├── wiki/                   # 【Agent 維護區】正式結構化 Markdown 知識頁面
│   ├── breeds/             # 品種百科與照護指南（如：馬爾濟斯、哈士奇、賓士貓等）
│   ├── health/             # 疾病預防、營養飲食、日常美容與健康管理
│   ├── behavior/           # 行為訓練、心理需求與環境豐富化
│   ├── concepts/           # 核心照護概念與跨物種通用知識
│   └── sources/            # 單篇 PDF 文獻的結構化閱讀筆記與重點摘要
└── slides/                 # 【視覺教學產出】正式獨立、無外部依賴的單一檔案 HTML5 教學簡報（檔名必須為繁體中文）
```

---

## 3. 頁面格式與連結慣例 (Page & Linking Conventions)

### 3.1 YAML Frontmatter（所有 `wiki/` 頁面必填，結構請參照 `templates/wiki-page-template.md`）
```yaml
---
title: 頁面標題
category: breeds | health | behavior | concepts | sources
tags: [標籤1, 標籤2, 寵物照護]
sources:
  - raw/檔名.pdf
last_updated: YYYY-MM-DD
status: active | needs-review | superseded
---
```

### 3.2 連結與結構規範
- **雙向連結**：頁面內部提及任何已存在或應建立的品種、疾病、行為概念時，一律使用標準相對路徑 Markdown 連結 `[顯示名稱](../category/filename.md)`，同時可保留 `[[頁面名稱]]` 標籤相容性（確保在 VS Code 與 Obsidian 皆可點擊跳轉）。
- **教學導向排版**：善用條列清單、重點提示框（`> 💡 **照護小叮嚀**`）、比較表格（Markdown Tables）與階段性步驟，避免冗長無分段的大段文字。
- **衝突標記**：若新加入的 PDF 數據或建議與既有頁面矛盾，必須在頁面中明確標註 `> ⚠️ **觀念更新 / 來源差異**`，並列明新舊來源依據。

---

## 4. 視覺美學與插畫風格指南 (Visual & Illustration Guidelines)

凡產出教學簡報（`slides/*.html`）、互動圖卡、或生成插畫/圖片時，必須嚴格遵守以下視覺規範，並以 `templates/slide-deck-template.html` 的排版與 CSS 架構為基準：

### 4.1 三色純淨色彩系統（Strict 3-Tone Light Palette）
整份簡報與視覺介面**嚴禁使用深色/重色背景**（包含封面與尾頁皆不得使用高飽和或深暗色塊），且全站僅限使用以下**三種純淨淡色背景**，避免視覺雜亂：
1. **封面背景（Cover Slide）**：低飽和淺藍 `#E6F0F5`（搭配邊框 `#B4CEDE`、強調色 `#8FB3C9`）。
2. **內容頁背景（Content Slides）**：統一使用溫暖奶油白 `#FAF8F5`（禁止混用其他灰白或冷白底色；卡片容器可搭配 `#E6F0F5` 淺藍底框或 `#E8F1EA` 淺綠底框作重點區隔）。
3. **尾頁與章節轉場背景（Ending / Section Divider Slides）**：低飽和鼠尾草綠 `#E8F1EA`（搭配邊框 `#B7D1BC`、強調色 `#8DAE93`）。
- **點綴暖色（Accent — 僅限小面積圖示/裝飾）**：溫潤淺駝色 `#D9B99B`。
- **文字色彩**：深暖灰 `#3A4348`（內文）、深藍灰 `#2C4251`（標題），禁用純黑 `#000000`。

### 4.2 封面插畫與圖片適配規範（Warm Watercolor Storybook Style & Content Fit）
每份教學簡報的**封面頁（Slide 1）必須包含一張實際可見的配圖**（嚴禁只放純文字封面），圖片檔案須同時備份至 `raw/assets/`（建議同步使用繁體中文檔名）並以 Base64 Data URI 內嵌於單一 HTML 檔案中（確保離線開啟絕不破圖）。所有配圖必須統一採用**溫馨手繪水彩繪本風**，且**高度適配簡報主題**：
- **主題適配原則（Content Relevance & Fit）**：
  - 若簡報為**單一品項／單一品種指南**（例如：《馬爾濟斯照護指南》），封面圖主角應精準對應該單一品種。
  - 若簡報為**綜合性／多品種入門教學**（例如：《新手適合養的狗狗全攻略》涵蓋小型犬與大型犬），封面圖**不可只放單一隻寵物**，必須呈現**多隻不同體型／品種的毛孩共同入鏡**（例如小型捲毛犬搭配大型黃金獵犬），使視覺主體與教學內容精準契合。
- **筆觸與質感**：柔和的鉛筆/棕色細線輪廓（Soft brown/charcoal ink outlines），搭配自然暈染的透明水彩上色（Gentle watercolor washes），保留紙張微肌理感。
- **角色與構圖**：寵物主角（犬貓等）神情親切微笑、圓潤可愛（Q版/繪本比例），常配戴鼠尾草綠或淺藍色小領巾；背景為簡約溫馨的居家一角（米色布沙發、淺藍抱枕、小盆栽、手繪小星星與綠葉藤蔓點綴），外框搭配圓角淺藍邊框（`border-radius: 20px; border: 3px solid #B4CEDE`）。
- **標準生圖提示詞模板（Image Generation Prompt Template）**：
  > `Warm hand-drawn watercolor storybook illustration of [單一或多位符合主題的寵物特徵與動作], wearing soft sage green bandanas, sitting on a cozy cream rug in a minimalist sunlit living room. Soft pastel blue curtains, a beige sofa with a pastel blue cushion, a small terracotta potted plant, delicate hand-drawn green leaves and tiny yellow stars floating around. Gentle brown ink outlines, soft watercolor washes, low-saturation pastel blue and sage green color palette, warm cream paper background, comforting and educational pet care aesthetic, no text.`

### 4.3 HTML 教學簡報檔名與結構規範 (`slides/<繁體中文簡報名稱>.html`)
- **簡報檔名強制繁體中文**：所有產出於 `slides/` 目錄下的正式簡報，**檔案名稱必須使用繁體中文**（例如：`slides/新手適合養的狗狗全攻略.html`、`slides/新手適合養的貓咪全攻略.html`），嚴禁使用純英文命名（`templates/` 內的參考骨架除外）。
- 生成新簡報時，務必複製並改寫 `templates/slide-deck-template.html` 的架構，確保為**單一檔案（Single-File HTML5 + CSS3 + Vanilla JS）**、零外部 CDN 依賴，並嚴格遵守 4.1 節的三色純淨背景分工與 4.2 節的封面配圖適配規定。

---

## 5.0 Ingest 前置檢查與內容證據閘門 (Preflight & Evidence Gate)
在原本 Auto-Ingest 開始前，先執行下列檢查：
1. 確認 PDF 可開啟並記錄頁數；嘗試文字抽取，若正文為空或明顯不完整，判定為掃描型 PDF，改採頁面轉圖、OCR 或人工抽查。
2. OCR 產生的品種名稱、專有名詞、數字、單位、疾病名稱及表格資料，未回看原頁確認前不得當成確定值寫入正式知識頁。
3. 來源筆記需記錄原始檔名、可辨識標題／來源、已讀取範圍、可支持的重點及待複核事項。無法確認的內容標記 `needs-review`。
4. Wiki 正式頁面的重要事實應能連回 `wiki/sources/` 的來源筆記；簡報內容應先通過來源依據與教學可理解性檢查，再進入 HTML 生成。
5. 來源品質檢查不通過時，回到 OCR／人工複核，不得以一般模型知識補齊並冒充原始 PDF 內容。

## 5. 標準作業流程與品質驗證迴圈 (Core Operations & Verification Loop)

### 5.1 全自動資料攝取 (`Auto-Ingest` — 偵測到 `raw/` 新增 PDF 時執行)
使用者將 PDF 放入 `raw/` 並下達攝取指令時，**無需中途停下詢問確認，直接自動完成以下所有步驟**：
1. **解析文獻**：完整讀取 PDF 內容，提取核心教學知識、照護數據、行為訓練步驟、注意事項與專業術語。
2. **建立來源筆記**：在 `wiki/sources/` 建立該 PDF 的完整結構化摘要頁（包含文獻基本資訊、核心重點、適用對象）。
3. **建立與更新知識頁面**：
   - 參照 `templates/wiki-page-template.md` 格式，檢查 `wiki/breeds/`、`wiki/health/`、`wiki/behavior/`、`wiki/concepts/` 中是否已有相關主題頁面。
   - 若已存在：將新知識無縫整合進既有頁面，更新 `last_updated` 與 `sources` 清單，並補強雙向連結。
   - 若不存在：為新出現的重要品種或核心照護主題建立獨立頁面。
4. **生成封面插畫與繁體中文命名教學簡報**：
   - 依據 4.2 節水彩繪本風與主題適配規範生成該主題封面插畫，存入 `raw/assets/`。
   - 參照 `templates/slide-deck-template.html` 在 `slides/` 生成**繁體中文檔名**的單一檔案 HTML 教學簡報（`slides/<繁體中文標題>.html`），將封面圖嵌入封面頁視覺區。
5. **更新索引與日誌**：
   - 更新 `index.md`，確保所有新增與修改的正式頁面（不含 `templates/`）皆有正確分類、連結與一句話教學摘要。
   - 在 `log.md` 最末端追加一行標準格式紀錄：
     `## [YYYY-MM-DD] ingest | <PDF檔名> -> 新增/更新了 <受影響頁面列表>`
6. **強制執行品質驗證迴圈（進入 5.2 節 Verification Loop）**，全數通過後才可向使用者回報與打包。

### 5.2 強制品質驗證與自動修復迴圈 (Mandatory Quality Verification Loop)
每次執行完 `Auto-Ingest`、`Query` 寫入或 `Lint` 後，Agent **必須自動進入以下五項檢查迴圈（Loop）**；若任一項目未通過（FAIL），**必須立即自動修正並重新驗證，直到 5 項全數通過（PASS）為止**：

1. **Loop Check 1 — 檔案路徑與目錄歸位檢查 (Directory Placement Check)**：
   - 確認原始 PDF 皆位於 `raw/`，圖片資源皆位於 `raw/assets/`。
   - 確認知識筆記依 `category` 精準放置於 `wiki/breeds/`、`wiki/health/`、`wiki/behavior/`、`wiki/concepts/` 或 `wiki/sources/`，無誤放於根目錄或其他錯誤資料夾。
   - 確認正式簡報位於 `slides/`，參考範本位於 `templates/` 且未被誤列入 `index.md`。
2. **Loop Check 2 — 簡報三色純淨配色檢查 (Slide Palette Audit)**：
   - 掃描 `slides/*.html` 的 CSS 與內聯樣式，驗證：
     - 封面背景色必為 `#E6F0F5`（低飽和淺藍）；
     - 所有內容頁背景色必為 `#FAF8F5`（溫暖奶油白），無混用其他灰白/冷白底色；
     - 尾頁背景色必為 `#E8F1EA`（低飽和鼠尾草綠）；
     - 整份簡報無任何深色/重色背景區塊或純黑 `#000000` 文字。
3. **Loop Check 3 — 封面圖存在、風格與主題適配度檢查 (Cover Image Existence, Style & Content Fit Audit)**：
   - 檢查每份 `slides/*.html` 的第 1 頁（`slide-cover`）是否包含有效的 `<img>` 標籤（非空路徑、非外部失效連結），且對應實體圖檔存在於 `raw/assets/`。
   - **視覺風格適配度**：確認圖片符合「溫馨手繪水彩繪本風（低飽和淺藍與鼠尾草綠配色、柔和棕色細線、奶油白紙張質感）」。
   - **主題內容適配度（Content Fit）**：比對簡報標題／教學範圍與封面圖主角（`alt` 屬性與實際圖像內容），確認物種與數量精準匹配（例如：綜合犬種入門簡報必須呈現多隻不同體型犬隻同框，不可只放單一品種；單一品項簡報則必須對應正確品種）。
4. **Loop Check 4 — 簡報繁體中文檔名檢查 (Slide Traditional Chinese Filename Audit)**：
   - 掃描 `slides/` 目錄下所有 `.html` 檔案，驗證每個檔名皆包含繁體中文字元且不含純英文命名，同時與該簡報 `<title>` 及 `index.md` 登記名稱一致。
5. **Loop Check 5 — 索引與雙向連結完整性檢查 (Index & Link Integrity Check)**：
   - 確認 `index.md` 已收錄所有正式 `wiki/` 與 `slides/` 檔案，無已刪除檔案的殘留連結，且所有相對路徑連結目標皆真實存在（無 Broken Links）。
   - 驗證通過後，於 `log.md` 記錄驗證結果（`## [YYYY-MM-DD] verify-loop | PASS (5/5 checks passed)`）。

**補充：Loop Check 6 — 內容來源依據檢查 (Evidence & Teaching Quality Check)**：
- 檢查簡報每個重要事實是否能回溯至 Wiki 頁面及其來源筆記。
- 檢查數字、專有名詞與健康照護建議是否有明確來源；未複核的 OCR 內容不得當成確定事實。
- 檢查教學順序是否由基本概念進展到實務應用，並確認初學者能理解必要名詞。
- 任一項未通過，回到 Query／大綱階段修正後重新檢查。

### 5.3 知識查詢與教學產出 (`Query`)
- 查詢時優先讀取 `index.md` 定位相關頁面，再深入讀取對應的 `wiki/` 頁面進行綜合解答，回答中必須附上資料來源連結。
- 若查詢結果具備高教學價值（例如：「新手養馬爾濟斯與哈士奇的照護差異比較表」），主動將整理好的結果寫入 `wiki/concepts/` 成為新的永久知識頁，並執行 5.2 節驗證迴圈。

### 5.4 知識庫健康檢查 (`Lint`)
當使用者要求執行 `Lint` 或定期維護時，自動掃描整個 `wiki/` 目錄並執行修復（孤兒頁面串聯、缺漏概念補齊、Frontmatter 與衝突標記檢查），並執行 5.2 節驗證迴圈。
