# 知識庫維護日誌 (Operation Log)

> 唯讀追加式紀錄（Append-Only），記錄每次資料攝取（ingest）、知識查詢沉澱（query）、健康檢查（lint）與品質驗證迴圈（verify-loop）。

## [2026-11-22] init | 初始化空白寵物教學 LLM Wiki 知識庫，建立 AGENTS.md 與 templates/ 參考範本
## [2026-11-22] ingest | 狗狗介紹.pdf -> 新增來源筆記 dog-breeds-guide.md、新手概念頁 beginner-friendly-dogs.md、健康頁 dog-common-health-issues.md、行為頁 dog-separation-anxiety-and-exercise.md、新手推薦犬種頁與教學簡報
## [2026-11-22] lint | 移除獨立比熊犬示範簡報與獨立品種頁 bichon-frise.md；將綜合犬種教學簡報重新命名為繁體中文 slides/新手適合養的狗狗全攻略.html，並更新封面插畫為小型捲毛犬與大型黃金獵犬雙犬種水彩繪本風（raw/assets/新手適合養的狗狗全攻略-封面.png）
## [2026-11-22] verify-loop | PASS (5/5 checks passed) — 通過目錄歸位、三色純淨配色、封面圖存在與多犬種主題適配度、簡報繁體中文檔名、索引與無斷裂連結檢查

## [2026-11-22] ingest | 貓咪介紹.pdf -> 新增來源筆記 cat-breeds-guide.md（初步 OCR 摘要，needs-review）
## [2026-11-22] ingest | 爬蟲介紹.pdf -> 新增來源筆記 reptile-care-guide.md（初步 OCR 摘要，needs-review）
## [2026-11-22] ingest | 鳥類介紹.pdf -> 新增來源筆記 bird-care-guide.md（初步 OCR 摘要，needs-review）
## [2026-11-22] ingest | 水族介紹.pdf -> 新增來源筆記 aquarium-fish-care-guide.md（初步 OCR 摘要，needs-review）
## [2026-11-22] workflow-update | 新增 Preflight、OCR／來源品質閘門、簡報內容依據檢查及失敗回退路徑；原因：五份 PDF 均為掃描型文件，一般文字抽取無法取得可用正文，OCR 有辨識錯誤風險
## [2026-11-22] reflection | 新增 REFLECTION.md，記錄本次最常出錯節點、將檢查前移至 ingest preflight，以及修改 graph 的原因
## [2026-11-22] verify-loop | PASS (結構檢查) — 五份 raw PDF 均有對應來源筆記、索引連結目標存在、Workflow／Reflection 文件已建立；四份新增來源筆記保留 needs-review，未宣稱完成逐頁校對
## [2026-11-22] lint | 從既有 HTML 的 Base64 封面圖還原 raw/assets/新手適合養的狗狗全攻略-封面.png，補齊原日誌所述的實體備份檔
