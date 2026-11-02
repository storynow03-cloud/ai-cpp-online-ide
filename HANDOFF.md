# HANDOFF.md - 專案交接與工作階段日誌

> 本文件遵循 GitHub `storynow01-arch/skill` 的 `shift-log` 慣例維護。
> 核心原則：交接文件是給「下一個對話的自己」看的，開工請動手驗證，收工請如實更新。

---

## 📌 目前現況摘要 (Last Updated: 2026-11-02)

- **專案狀態**：專案初始化與規範正規化完成（Stage 0 -> Stage 1）
- **Git 狀態**：本地初始化完成，初始基礎規範設定完畢
- **服務/Process**：尚未啟動任何常駐服務（處於規格與架構規劃階段）
- **資安檢核**：`.gitignore` 與 `.env.example` 設置完畢，無硬編碼金鑰，環境安全
- **當前核心目標**：完成 C++ 線上 IDE 的技術架構評估與規格制定（/spec 與 /plan）
- **帳號綁定規範**：全專案（GitHub, Vercel, Supabase）統一指定使用 `storynow03` (`storynow03@gmail.com`) 帳戶操作
  - GitHub CLI：✅ 已切換為作用中帳戶 `storynow03-cloud`
  - 本地 Git：✅ 已設定 `user.name = "storynow03-cloud"`、`user.email = "storynow03@gmail.com"`
  - Vercel CLI：✅ 已成功切換為作用中帳戶 `storynow03-cloud`
  - Supabase CLI：✅ 已成功授權登入（帳號：`storynow03@gmail.com`，已成功連線）

---

## ⛔ 煞車點決策樹 (Next Step Decision Tree)

【待決策煞車點】：確認 C++ 線上 IDE 的核心技術棧與架構路線
- **路線 A（純前端 WebAssembly 編譯 - 零伺服器成本、極致安全）**：
  - 特點：利用 Clang/LLVM WebAssembly (如 wasm-clang / webassembly.sh) 直接在使用者瀏覽器中編譯與執行 C++。
  - 優勢：完全不需後端編譯伺服器，零沙盒逃逸風險，伺服器頻寬與算力成本為 0，適合教學與基礎競賽題解。
  - 限制：編譯速度受本機瀏覽器性能限制，不支援部分多線程或 POSIX 原生 socket 等深度底層系統呼叫。
- **路線 B（輕量後端 Docker/Nsjail 沙盒編譯 - 完整 Linux 原生功能）**：
  - 特點：Node.js / Python 後端接收程式碼，呼叫 Nsjail 或 Docker 容器限制 CPU、記憶體與網路執行原生 `g++`。
  - 優勢：完整支援 C++20/C++23、標準函式庫與 Linux 系統程式設計。
  - 限制：需要後端伺服器與嚴密沙盒安全隔離，維運成本較高。
- **路線 C（混合架構 - WebAssembly 優先，進階呼叫雲端沙盒）**：
  - 特點：平日練習用 WebAssembly 本機即時反饋，遇到特定大型或系統呼叫需求時切換雲端沙盒。

---

## 📝 進度日誌 (Shift Log)

### 2026-11-02（三大雲端環境 storynow03 全數完成就緒）
- **做了什麼**：
  - 驗證 GitHub CLI、Vercel CLI、Supabase CLI 均已成功切換並授權至 `storynow03`。
  - Supabase 成功讀取 `storynow03` 專案清單（CAP / CAP-review），API 連線正常。
  - 全專案準備進入實作階段。

### 2026-11-02（帳號全面切換至 storynow03@gmail.com）
- **做了什麼**：
  - 依照指示將專案目標帳號統一變更為 `storynow03@gmail.com`。
  - GitHub CLI 直接透過 `gh auth switch -u storynow03-cloud` 切換為作用中帳號，並將本地 Git commit 作者綁定為 `storynow03-cloud` / `storynow03@gmail.com`。
  - 記錄 Vercel 與 Supabase 登入指引。

### 2026-11-02（帳號環境檢核與工具鏈安裝）
- **做了什麼**：
  - 檢測開發工具鏈（GitHub CLI、Vercel CLI、Supabase CLI）之安裝與帳號登入狀態。
  - 完成安裝 Supabase CLI 全域版本 (`v2.122.0`)。
  - 確立本專案全工具鏈統一指向 `storynow04` 之規範。

### 2026-11-02（階段初始化與工程規範正規化）
- **做了什麼**：
  1. 檢視使用者 GitHub 帳號 (`storynow01-arch`) 之 Skill 收藏庫（`shift-log`、`user-agreement`、`agent-skills` 等）。
  2. 依據工程與資安規範正規化專案：
     - 建立標準 `.gitignore`，包含機密過濾、編譯暫存、沙盒執行防護。
     - 建立 `.env.example` 環境變數範本。
     - 建立 `AGENTS.md` 與 `CLAUDE.md`，注入 Addy Osmani 開發生命週期規範與繁體中文規範。
     - 建立 `HANDOFF.md` 交接日誌機制。
     - 規劃專案標準目錄架構（`docs/`、`frontend/`、`backend/`、`tests/`）。
     - 撰寫完整繁體中文 `README.md`。
- **為什麼這樣做**：
  - 遵循資安第一 (Security First) 與高標準軟體工程規範，確保專案從起步階段就有嚴謹的邊界考量與日誌傳承，避免後續架構失控或機密洩漏。
- **下一步指示**：
  - 等待使用者確認架構決策（路線 A / B / C），進入 `/spec` 階段細化架構圖與 API 規格。
