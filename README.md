# C++ 線上 IDE (C++ Online IDE)

> 現代化、輕量且具備安全隔離機制的 C++ 線上編譯與即時運行平台。

---

## 📖 專案概述

本專案旨在提供一個針對程式設計教學、競賽題解（CPE / APCS / LeetCode）與快速驗證演算法的 **C++ 線上整合開發環境 (Online IDE)**。
使用者只需透過瀏覽器即可享受現代化的程式碼編輯、語法高亮、即時自動補全、標準輸入輸出 (I/O) 模擬，以及安全的編譯與執行反饋。

---

## ✨ 核心特色與架構規劃

1. **現代化編輯器體驗**：
   - 採用 Monaco Editor（VS Code 核心）提供專業的語法高亮、智慧提示、縮排與快捷鍵支援。
   - 支援 C++11 / C++14 / C++17 / C++20 / C++23 等多種語言標準選擇。
   - 支援自訂標準輸入 (stdin) 與執行參數。

2. **多維度執行架構（依需求調配）**：
   - **純前端 WebAssembly (Wasm) 執行**：無伺服器成本、零網路延遲、本機極致安全。
   - **雲端沙盒隔離執行 (Docker / Linux Namespace / Nsjail)**：提供完整 Linux 原生 `g++` / `clang++` 環境，支援多執行緒與系統層呼叫。

3. **🛡️ 嚴格沙盒安全隔離**：
   - **CPU / 執行時間限制**：防止無限迴圈（Timeout 機制）。
   - **記憶體限制**：防止惡意申請記憶體或 Memory Leak (OOM 限制)。
   - **行程數量限制 (pids limit)**：完全防堵 Fork Bomb 攻擊。
   - **檔案系統唯讀隔離**：禁止未授權讀寫主機敏感檔案。
   - **網路隔離**：執行環境禁止連外，防範惡意探測或反向 Shell。

4. **高標準軟體工程規範**：
   - 遵循 [Addy Osmani Agent Skills](https://github.com/storynow01-arch/agent-skills) 之生命週期規範 (`/spec` -> `/plan` -> `/build` -> `/test` -> `/review`)。
   - 導入 [shift-log](https://github.com/storynow01-arch/skill) 跨對話交接日誌機制 ([`HANDOFF.md`](HANDOFF.md))。
   - 嚴格遵守資安優先 (Security First) 原則，禁止 Hardcode 機密與敏感金鑰。

---

## 📂 專案目錄結構

```text
C++線上IDE/
├── .github/                 # GitHub Actions CI/CD 與自動化工作流
├── docs/                    # 專案架構、規格文件與 PRD
│   ├── spec.md              # 系統需求規格書 (/spec)
│   ├── architecture.md      # 系統架構與資料流設計
│   └── security-sandbox.md  # 沙盒安全與防禦機制設計
├── frontend/                # 前端 Web 應用 (React / Next.js + Monaco Editor)
│   ├── src/                 # 前端原始碼
│   └── public/              # 靜態資源與 Wasm 編譯器檔案
├── backend/                 # 後端編譯調度 API (若採用雲端沙盒架構)
│   ├── src/                 # API 伺服器
│   └── sandbox/             # 沙盒執行腳本與限制策略
├── tests/                   # 單元測試、邊界測試與安全防護測試
├── .env.example             # 環境變數設定範本（安全隔離）
├── .gitignore               # 嚴密排除機密與編譯產物
├── AGENTS.md                # AI 協同開發代理人守則
├── CLAUDE.md                # 開發快速指引
├── HANDOFF.md               # 開工與收工工作階段交接日誌
└── README.md                # 專案總覽文件
```

---

## 🚀 開發指引

### 環境需求
- **Node.js**：v18+ (推薦 v20 LTS 或 v24)
- **套件管理器**：npm / pnpm
- **Python / 工具**（若後端或工具鏈使用）：使用 `uv` 建立虛擬環境（`uv venv`），嚴禁全域污染

### 快速開始
1. **複製環境設定檔**：
   ```bash
   cp .env.example .env
   ```
2. **安裝前端相依套件**（待前端專案建置）：
   ```bash
   cd frontend && npm install
   ```
3. **啟動開發伺服器**：
   ```bash
   npm run dev
   ```

---

## 📜 授權條款與致謝
- 本專案採用 MIT 授權條款。
- 工作流程靈感源自 GitHub [`storynow01-arch/skill`](https://github.com/storynow01-arch/skill) 與 [`storynow01-arch/agent-skills`](https://github.com/storynow01-arch/agent-skills)。
