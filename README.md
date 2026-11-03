# USB PD Spec Guide ・ USB PD 規範導覽手冊

**[繁體中文](#繁體中文) ｜ [English](#english)**

🔗 Live / 線上版：<https://tedchen0814.github.io/usb-pd-spec-summary/> （mirror / 備援：<https://usb-pd-spec-summary.vercel.app>）
English view / 英文版：<https://tedchen0814.github.io/usb-pd-spec-summary/?lang=en>

---

## 繁體中文

### 這是什麼
依 **USB Power Delivery R3.2 V1.2**（2026-05 版）與 **USB Type-C R2.4**（2025-10 版）整理的互動式導覽手冊。單頁靜態網站，不需安裝、不需後端，用瀏覽器直接開。目標是讓韌體／硬體工程師能快速查到規格重點，並用動畫與小工具理解協商流程。

### 內容（19 章，依主題分六組）
- **規格導讀**（Ch1–3）：簡介與版本對照、術語、端口電源需求。
- **電氣與訊號**（Ch4–6）：電氣需求、物理層架構、BMC 訊號編碼與電氣特性。
- **訊息與資料物件**（Ch7–10）：協定訊息、PDO / RDO 詳解、PPS、12V PDO 特殊考量。
- **供電角色與 CC 偵測**（Ch11–16）：PD Source 與 Rp/Rd、PD Sink、DRP 雙角色與 Try.SRC/Try.SNK、Type-C 腳位與設備偵測、Dead Battery 與 5.1kΩ Rd、Fast Role Swap（FRS）。
- **線纜與擴充**（Ch17–18）：Alternate Mode、E-Marker 與線纜通訊。
- **實務與交付**（Ch19 ＋ 附錄）：FW 設計規格與 Check List、相關專案、修改歷史紀錄。

每章開頭有「30 秒重點」(TL;DR)。

### 互動工具
| 位置 | 工具 |
|---|---|
| Chapter 6 | BMC 封包編碼器（含 4b5b 與 CRC-32 檢查） |
| Chapter 7 | 互動式封包結構圖 |
| Chapter 8 | PDO / RDO 協商流程動畫、PDO/RDO 32-bit 欄位解碼器 |
| Chapter 11 | CC 電壓偵測（Rp / Rd / Ra 組合與電流宣告） |
| Chapter 13 | DRP Try.SRC / Try.SNK 狀態動畫 |
| Chapter 15 | Dead Battery 步進動畫（DRP Rp/Rd 切換、TPS66994C 箝位） |
| Chapter 16 | FRS 時序圖（150µs 內完成切換的兩種情境） |

另有分組側邊目錄、全文搜尋（按 `/` 聚焦）。

### 雙語（中／EN）
頁首右上角按鈕切換，選擇會記在瀏覽器（localStorage `pd-lang`），也可用網址參數 `?lang=en` / `?lang=zh`。中文為原文，英文字典在 `lang-en.js`。

### 專案結構
```
index.html     全部內容、樣式與互動（單檔，內嵌 CSS / JS）
lang-en.js     英文字典（window.PD_EN；鍵 = 中文內容的雜湊）
.github/workflows/pages.yml   GitHub Pages 部署
```
`index.html` 與 `lang-en.js` 必須一起部署，否則英文版無法使用（頁面會維持中文）。

### 本機執行
純靜態，任一靜態伺服器皆可，例如：
```bash
python -m http.server 8000
```
再開啟 <http://localhost:8000/>。

### 維護者備註
- 章節網址錨點 `#ch1`～`#ch19` 沿用舊編號；畫面上的 Chapter 編號依主題重排，兩者不同（例如 Dead Battery 錨點 `#ch18`、畫面 Chapter 15）。
- 修改中文原文後，該段英文會退回中文顯示；在瀏覽器 console 執行 `PDI18N.missing()` 可列出尚未翻譯的項目。
- 互動工具內的 JS 字串用 `_t("中文")`（可帶 `{變數}`），重繪時掛 `PDI18N.onChange`。
- 推送到 `master` 會自動部署 GitHub Pages（Vercel 亦同步更新）。

### 規格依據與免責
數值（計時器、電壓、欄位定義）依上述規格版本整理，但為**學習用摘要**，不取代正式規格；設計與認證請以 USB-IF 官方文件為準。若發現錯誤，歡迎開 Issue。本專案與 USB-IF 無關。

### 相關專案
- [pd-packet-decoder](https://github.com/tedchen0814/pd-packet-decoder)：PD 封包解碼工具。
- [USB-PD-FW-Checklist](https://github.com/tedchen0814/USB-PD-FW-Checklist)：USB PD 韌體檢查清單。

---

## English

### What is this
An interactive guide to **USB Power Delivery R3.2 V1.2** (May 2026) and **USB Type-C R2.4** (Oct 2025). It is a single-page static site: no install, no backend, just open it in a browser. It is meant for firmware/hardware engineers who want quick spec look-ups, plus animations and small tools that make the negotiation flow easy to follow.

### Contents (19 chapters in six topic groups)
- **Spec Overview** (Ch1–3): introduction and version comparison, glossary, port power requirements.
- **Electrical & Signaling** (Ch4–6): electrical requirements, physical-layer architecture, BMC coding and electrical characteristics.
- **Messages & Data Objects** (Ch7–10): protocol messages, PDO / RDO in detail, PPS, special considerations for the 12V PDO.
- **Power Roles & CC Detection** (Ch11–16): PD Source and Rp/Rd, PD Sink, DRP with Try.SRC/Try.SNK, Type-C pins and device detection, Dead Battery and the 5.1kΩ Rd, Fast Role Swap (FRS).
- **Cables & Extensions** (Ch17–18): Alternate Mode, E-Marker and cable communication.
- **Practice & Delivery** (Ch19 + appendices): FW design spec and delivery checklist, related projects, changelog.

Every chapter starts with a "30-second summary" (TL;DR).

### Interactive tools
| Where | Tool |
|---|---|
| Chapter 6 | BMC packet encoder (with 4b5b and CRC-32 check) |
| Chapter 7 | Interactive packet-structure diagram |
| Chapter 8 | PDO / RDO negotiation animation and a 32-bit PDO/RDO field decoder |
| Chapter 11 | CC voltage detection (Rp / Rd / Ra combinations and current advertisement) |
| Chapter 13 | DRP Try.SRC / Try.SNK state animation |
| Chapter 15 | Dead Battery step-by-step animation (DRP Rp/Rd toggling, TPS66994C clamp) |
| Chapter 16 | FRS timing diagram (two scenarios against the 150 µs budget) |

Also included: a grouped side table of contents and full-text search (press `/` to focus).

### Bilingual (中 / EN)
Use the button at the top right of the header. The choice is stored in the browser (localStorage `pd-lang`); you can also use the URL parameter `?lang=en` or `?lang=zh`. Chinese is the source text; English strings live in `lang-en.js`.

### Project layout
```
index.html     all content, styles and interactivity (single file, inline CSS / JS)
lang-en.js     English dictionary (window.PD_EN; key = hash of the Chinese source)
.github/workflows/pages.yml   GitHub Pages deployment
```
`index.html` and `lang-en.js` must be deployed together; without the dictionary the page stays in Chinese.

### Run locally
Any static server works, for example:
```bash
python -m http.server 8000
```
Then open <http://localhost:8000/>.

### Maintainer notes
- Chapter URL anchors `#ch1`–`#ch19` keep the old numbering, while the chapter numbers shown on screen were re-ordered by topic (e.g. Dead Battery is anchor `#ch18` but displayed as Chapter 15).
- After editing a Chinese source string, its English text falls back to Chinese; run `PDI18N.missing()` in the browser console to list untranslated items.
- JS strings inside the tools use `_t("中文")` (optionally with `{vars}`), and tools re-render through `PDI18N.onChange`.
- Pushing to `master` redeploys GitHub Pages (Vercel updates as well).

### Spec basis & disclaimer
Values (timers, voltages, field definitions) follow the spec versions above, but this is a **study summary** and does not replace the official specifications; for design and certification, use the official USB-IF documents. Please open an Issue if you spot an error. This project is not affiliated with USB-IF.

### Related projects
- [pd-packet-decoder](https://github.com/tedchen0814/pd-packet-decoder): PD packet decoder.
- [USB-PD-FW-Checklist](https://github.com/tedchen0814/USB-PD-FW-Checklist): USB PD firmware checklist.
