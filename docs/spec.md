# 規格書：C++ 線上 IDE (System Specification)

> 規範階段：/spec  
> 依據：[Addy Osmani - Spec Driven Development](https://github.com/storynow01-arch/agent-skills/tree/main/skills/spec-driven-development)  
> 狀態：草案 (Draft) / 待煞車點確認

---

## 1. 問題陳述 (Problem Statement)
學習 C++ 或進行演算法刷題（如 APCS、CPE、LeetCode）時，初學者常遇到環境建置繁瑣（如 MinGW、WSL、VS Code 設定困難）等門檻。線上 IDE 能讓學習者開箱即用。
然而，線上編譯執行 C++ 有著極高資安風險：
- 執行未受信任程式碼可能導致主機被滲透、耗盡系統資源、遭受 Fork Bomb 攻擊或惡意連外。
- 需要在「使用者體驗（快速反應、編輯手感）」與「安全隔離（沙盒防禦）」之間取得平衡。

---

## 2. 目標與非目標 (Goals & Non-Goals)

### 目標 (Goals)
- 提供現代化網頁編輯介面（支援 Monaco Editor、深色主題、語法突顯、行號、自訂字體大小）。
- 提供一鍵編譯與執行功能，並即時回傳 stdout、stderr、編譯錯誤及執行時間與記憶體使用量。
- 支援標準輸入 (stdin) 互動（支援需要自訂測資的演算法練習）。
- 提供安全隔離沙盒機制（時間超時中斷、記憶體上限、禁止危險系統呼叫與網路連線）。
- 支援常用 C++ 標準庫（STL、`<iostream>`、`<vector>`、`<algorithm>`、`<map>` 等）。

### 非目標 (Non-Goals)
- 第一階段不支援圖形化視窗輸出（如 GUI、SDL、OpenGL 視窗）。
- 第一階段不支援長期背景常駐服務或網路 socket 監聽。

---

## 3. 功能需求 (Functional Requirements)

1. **程式碼編輯模組**：
   - 預設提供 Hello World 或標準 APCS/CPE 範本。
   - 快速切換 C++ 版本（C++17 為推薦預設值，支援 C++11, C++20）。
   - 快捷鍵支援（如 `Ctrl+Enter` / `Cmd+Enter` 一鍵編譯執行）。
2. **測資輸入/輸出介面**：
   - 獨立的 Stdin 輸入區塊（支援多行測資）。
   - 清楚區分「編譯訊息」、「執行輸出 (stdout)」與「錯誤輸出 (stderr)」。
   - 顯示執行耗時（ms）與回傳狀態碼 (Exit Code)。
3. **錯誤提示與診斷**：
   - 解析 GCC/Clang 報錯資訊，標示錯誤行號與具體原因。
4. **程式碼分享與儲存 (選配)**：
   - 可導出 `.cpp` 檔案或生成唯讀分享連結。

---

## 4. 非功能需求 (Non-Functional Requirements)

- **安全性 (Security)**：
  - CPU Timeout：最長 5000ms（防止死迴圈）。
  - Memory Limit：最高 256MB。
  - Process Limit：最多限制 1 個衍生行程（防止 Fork Bomb）。
  - 網路：執行環境完全封鎖網路對外連線。
- **效能 (Performance)**：
  - 編譯與啟動回應時間應小於 2 秒（若為 WebAssembly 則接近即時）。
- **可用性 (Usability)**：
  - 響應式介面，支援桌面端與平板寬螢幕操作。
