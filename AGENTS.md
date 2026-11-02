# AGENTS.md - C++ 線上 IDE 開發指南與代理人守則

本文件為 AI 代理人（Antigravity、Claude Code、Cursor 等）協同開發此專案時的核心遵循規範。所有代理人在此專案中執行任何任務均需嚴格遵守以下準則。

---

## 🧭 核心開發哲學與模式

### 1. 預設開發模式 (Addy Osmani Skills 優先)
涉及系統開發、架構規劃、寫程式、重構、除錯、部署時，強制套用高標準軟體工程實踐：
- **動手前必先規格與計畫 (Spec & Plan)**：不允許直接跳入寫程式，必須先拆解任務、定義規格與驗收條件。
- **邊界考量與單元測試**：包含邊界條件處理與測試驗證，嚴禁以「稍後再補上」為由跳過測試。
- **開發生命週期映射**：
  - `/spec`：定義目標與需求規格 (`spec-driven-development`)
  - `/plan`：任務分解與循序漸進架構 (`planning-and-task-breakdown`)
  - `/build`：增量建置與最小切片實作 (`incremental-implementation`)
  - `/test`：以測試為憑證，嚴格驗證 (`test-driven-development`)
  - `/review`：程式碼審查、資安稽核與簡化 (`code-review-and-quality`)

### 2. 開工與收工工作階段慣例 (`shift-log`)
本專案導入 GitHub Skills 庫之 `shift-log` 規範：
- **開工 (Session Start)**：
  1. 讀取專案交接文件 [`HANDOFF.md`](file:///d:/antigravity/C%2B%2B%E7%B7%9A%E4%B8%8AIDE/HANDOFF.md)。
  2. 動手驗證環境狀態（檢查 git status、port、process、.gitignore 防線、uv/.venv 環境），不照單全收。
  3. 提供簡短「3 秒現況儀表板」回報。
- **收工 (Session End)**：
  1. 整理本次成果、決策動機與「為什麼選此方案」。
  2. 記錄遇到的問題與根本原因。
  3. 寫下清晰可直接執行的「下一步指示」及「煞車點決策樹」。
  4. 更新 [`HANDOFF.md`](file:///d:/antigravity/C%2B%2B%E7%B7%9A%E4%B8%8AIDE/HANDOFF.md) 進度日誌與開頭現況摘要。
  5. 執行資安掃描，確認無機密外洩。

---

## 🛡️ 資安與執行安全準則 (Security First)

1. **嚴禁 Hardcode 金鑰與密碼**：
   - 任何 API Key、Secret、連線字串均需存放於 `.env`。
   - 嚴格維持 `.gitignore` 的排除防線。
   - 交付前執行全局關鍵字掃描（`API_KEY|SECRET|PASSWORD|TOKEN`）。
2. **C++ 線上編譯與執行的沙盒安全（重要）**：
   - 使用者提交的 C++ 原始碼為不可信任輸入（Untrusted Input）。
   - 編譯與執行必須處於嚴密沙盒（Sandbox）或隔離容器內：
     - **CPU / 執行時間限制**（防止死迴圈）
     - **記憶體限制**（防止記憶體洩漏與耗盡）
     - **行程數量限制 (pids limit)**（防止 Fork Bomb）
     - **檔案系統唯讀或臨時掛載**（防止讀取伺服器機密或破壞 host 檔案）
     - **網路隔離**（阻斷對外連線，防範反向 Shell 與內網探測）

---

## 🌐 語言與工程環境慣例

- **預設語言**：繁體中文（台灣用語），包含文檔、註解、思考過程與 commit 訊息。
- **Python 開發**：若後端或工具腳本使用 Python，**強制使用 uv 與 .venv** 虛擬環境，嚴禁使用系統 base 環境或單獨全域 pip。
- **可點擊連結規範**：所有檔案與符號引用需使用標準 `file://` 協定連結。
