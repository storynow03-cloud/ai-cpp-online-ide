# CLAUDE.md - C++ 線上 IDE 開發指引

## 專案概要
- **專案名稱**：C++ 線上 IDE (C++ Online IDE)
- **核心目標**：提供輕量、流暢、具備現代化編輯體驗且具備高安全沙盒機制的 C++ 線上編譯與即時運行平台。
- **規範參考**：
  - 開工 / 收工日誌慣例：參照 GitHub `storynow01-arch/skill` 之 `shift-log`
  - 軟體工程實踐：參照 `storynow01-arch/agent-skills` 之 Addy Osmani 開發生命週期
  - 資安第一：機密隔離、環境變數管制、未受信任程式碼沙盒防護

## 常用指令速查
- **開工確認**：檢查 [`HANDOFF.md`](file:///d:/antigravity/C%2B%2B%E7%B7%9A%E4%B8%8AIDE/HANDOFF.md)、git status、.env 與環境隔離
- **收工紀錄**：整理任務摘要、煞車點決策樹並寫回 [`HANDOFF.md`](file:///d:/antigravity/C%2B%2B%E7%B7%9A%E4%B8%8AIDE/HANDOFF.md)
- **環境管理**：
  - Python 工具：`uv venv`、`uv run <command>`（切勿使用全域 pip）
  - 前端套件：`npm run dev` / `npm test` / `npm run build`
- **資安掃描**：收工或 commit 前執行機密掃描

## 關鍵規範
- 全程使用繁體中文（台灣用語）撰寫文件與對話。
- 遵循高標準測試與邊界覆蓋。
- 交付前務必確保無金鑰外洩。
