<!--
  同步影響報告 (Sync Impact Report)
  ===================================
  版本變更: 0.0.0 → 1.0.0
  變更類型: MAJOR - 首次建立專案憲法

  新增章節:
  - 核心原則 (5項)
  - 技術約束
  - 開發流程
  - 治理規範

  模板更新狀態:
  - .specify/templates/spec-template.md: ✅ 已更新為中文版
  - .specify/templates/plan-template.md: ✅ 已更新為中文版
  - .specify/templates/tasks-template.md: ✅ 已更新為中文版
  - .specify/templates/checklist-template.md: ✅ 已更新為中文版
  - .specify/templates/agent-file-template.md: ✅ 已更新為中文版

  待辦事項: 無
-->

# TravelApp 旅遊行程助手 專案憲法

## 核心原則

### I. 行動優先 PWA (Mobile-First PWA)

本專案以 iPhone 使用者為主要對象，所有設計決策必須優先考量行動裝置體驗。

- 所有 UI 設計必須以 iPhone 螢幕尺寸 (375px-428px) 為優先
- 必須支援「加入主畫面」功能，提供類原生 App 體驗
- 必須實作 Service Worker 以支援離線存取核心功能
- 觸控操作優先，確保按鈕尺寸至少 44x44px
- 手勢操作必須流暢自然，避免複雜的多指操作

### II. 資料層抽離 (Data Layer Abstraction)

為確保未來可平滑遷移至雲端同步方案，資料存取架構必須保持抽象化。

- 所有資料存取必須透過統一的 Repository 介面
- 初期實作使用 IndexedDB（透過 Dexie.js 封裝）
- 架構必須支援未來切換至 Firebase 而不影響業務邏輯層
- 資料模型 (Models) 與儲存實作 (Repositories) 必須完全分離
- 禁止在 UI 元件中直接操作資料庫

### III. 日式極簡設計 (Japanese Minimalist Design)

視覺設計遵循日式極簡美學，強調留白與功能性。

- 大量留白，建立清晰的視覺層次與呼吸感
- 色彩必須克制，以中性色（白、灰、黑）為主調
- 重點資訊使用強調色標示，但同一畫面不超過 3 種強調色
- 字體必須清晰易讀，中文使用系統預設字體，行距至少 1.5 倍
- 動畫必須簡潔自然（200-300ms），禁止過度裝飾性動效
- 卡片設計採用圓角（8-12px）與輕微陰影，營造層次感

### IV. 離線優先 (Offline-First)

作為旅遊應用，必須確保在網路不穩定環境下仍能正常使用。

- 核心行程資料必須可完全離線存取
- 天氣預報、導遊資訊等外部資料必須實作快取機制
- 無網路連線時必須顯示快取資料，並明確標示最後更新時間
- 外部 API 呼叫失敗時必須優雅降級，不得影響核心功能
- 網路恢復時應自動同步更新，無需使用者手動操作

### V. 元件單一職責 (Single Responsibility Components)

Vue 元件設計遵循單一職責原則，確保可維護性與可重用性。

- 每個 Vue 元件只負責一個明確的功能
- 卡片類型（景點、餐廳、交通）必須各自獨立設計，共用基礎樣式
- 元件必須可組合、可重用，避免巨型元件
- 業務邏輯應抽離至 Composables 或 Services
- 元件 Props 必須定義明確的 TypeScript 型別

## 技術約束

### 技術棧規範

| 層級 | 技術 | 版本要求 |
|------|------|----------|
| 框架 | Vue 3 + Composition API | ^3.4 |
| 語言 | TypeScript | ^5.0 |
| 建構工具 | Vite | ^5.0 |
| 狀態管理 | Pinia | ^2.1 |
| 路由 | Vue Router | ^4.2 |
| 資料儲存 | Dexie.js (IndexedDB) | ^4.0 |
| PWA | vite-plugin-pwa | ^0.17 |
| HTTP 客戶端 | Fetch API | 原生 |

### 外部服務

| 服務 | 用途 | 方案 |
|------|------|------|
| OpenWeatherMap | 天氣預報 | 免費方案 (1000 次/月) |
| OpenAI API | 導遊 AI 分析 | 按量計費（混合模式，可手動輸入替代） |
| Google Maps / Apple Maps | 導航 | URL Scheme（免費） |

### 禁止事項

- 禁止引入 jQuery 或其他 DOM 操作函式庫
- 禁止使用 CSS 框架（如 Bootstrap、Tailwind），必須使用自訂 CSS Variables
- 禁止在元件中直接呼叫 IndexedDB API，必須透過 Repository
- 禁止硬編碼 API Keys，必須使用環境變數

## 開發流程

### 規格驅動開發

本專案採用 Spec-Kit 規格驅動開發流程：

1. `/speckit.constitution` - 定義專案憲法（本文件）
2. `/speckit.specify` - 定義功能規格
3. `/speckit.plan` - 制定技術計畫
4. `/speckit.tasks` - 生成任務清單
5. `/speckit.implement` - 執行實作

### 分支策略

- `main` - 主分支，保持可部署狀態
- `{編號}-{功能名稱}` - 功能分支，例如 `001-trip-management`

### 提交規範

提交訊息格式：`<類型>: <描述>`

類型包含：
- `feat` - 新功能
- `fix` - 修復錯誤
- `docs` - 文件更新
- `style` - 樣式調整（不影響程式邏輯）
- `refactor` - 重構
- `test` - 測試相關
- `chore` - 維護性工作

## 治理規範

### 憲法修訂程序

1. 提出修訂需求與理由
2. 評估對現有功能的影響
3. 更新憲法文件並同步所有相關模板
4. 版本號遵循語意化版本：
   - MAJOR: 移除或重新定義核心原則
   - MINOR: 新增原則或章節
   - PATCH: 文字修正或澄清

### 合規審查

- 所有 PR 必須確認符合核心原則
- 複雜度增加必須提供合理化說明
- 設計決策應參照本憲法原則

**版本**: 1.0.0 | **建立日期**: 2025-11-27 | **最後修訂**: 2025-11-27
