# Spec-Kit 規格驅動開發流程指南

## 概述

Spec-Kit 是 GitHub 開發的規格驅動開發工具，核心理念是「先定義需求，再實作程式碼」，透過 AI 助手根據清晰的規格文檔自動生成工作代碼。

---

## 工作流程步驟

### Step 1: `/speckit.constitution` - 建立專案憲法

**目的**: 定義專案的基本原則、技術約束和治理規範

**執行時機**: 專案初始化時，只需執行一次

**產出檔案**: `.specify/memory/constitution.md`

**內容包括**:
- 專案目標與願景
- 技術棧選擇 (前端/後端/資料庫)
- 程式碼風格規範
- 安全性要求
- 團隊約定與限制

---

### Step 2: `/speckit.specify` - 定義需求規格

**目的**: 將功能需求轉換為清晰的用戶故事和驗收標準

**執行時機**: 開始新功能前

**產出檔案**: `.specify/specs/<feature-name>.md`

**內容包括**:
- 功能描述
- 用戶故事 (As a... I want... So that...)
- 驗收標準 (Acceptance Criteria)
- 邊界條件與例外處理

---

### Step 3: `/speckit.plan` - 制定技術計劃

**目的**: 將需求規格轉換為具體的技術實現方案

**執行時機**: 需求規格確認後

**產出檔案**: `.specify/plans/<feature-name>.md`

**內容包括**:
- 系統架構設計
- 資料模型設計
- API 設計
- 檔案結構規劃
- 相依性分析

---

### Step 4: `/speckit.tasks` - 生成任務清單

**目的**: 將技術計劃拆分為可執行的開發任務

**執行時機**: 技術計劃確認後

**產出檔案**: `.specify/tasks/<feature-name>.md`

**內容包括**:
- 任務清單 (含優先順序)
- 每個任務的預估範圍
- 任務之間的相依關係
- 驗證方式

---

### Step 5: `/speckit.implement` - 執行實作

**目的**: 按照任務清單逐一實作程式碼

**執行時機**: 任務清單確認後

**流程**:
1. 按順序執行每個任務
2. 每完成一個任務進行驗證
3. 更新任務狀態
4. 處理發現的問題

---

## 其他輔助指令

| 指令 | 用途 |
|------|------|
| `/speckit.analyze` | 分析現有程式碼結構 |
| `/speckit.clarify` | 釐清不明確的需求 |
| `/speckit.checklist` | 生成/檢查完成清單 |
| `/speckit.taskstoissues` | 將任務轉換為 GitHub Issues |

---

## 目錄結構

```
.specify/
├── memory/
│   └── constitution.md      # 專案憲法
├── specs/
│   └── <feature>.md         # 功能規格
├── plans/
│   └── <feature>.md         # 技術計劃
├── tasks/
│   └── <feature>.md         # 任務清單
├── templates/               # 模板檔案
└── scripts/                 # 輔助腳本

.claude/
└── commands/                # Claude 斜線指令定義
```

---

## 最佳實踐

1. **循序漸進**: 按照 constitution → specify → plan → tasks → implement 的順序執行
2. **充分討論**: 每個階段完成後與 AI 確認，確保理解一致
3. **版本控制**: 每個階段完成後進行 git commit
4. **持續更新**: 需求變更時更新對應的規格文件
5. **保持簡潔**: 規格文件應清晰易讀，避免過度複雜

---

## 快速開始範例

```bash
# 1. 初始化專案
specify init my-project --ai claude

# 2. 進入專案目錄
cd my-project

# 3. 啟動 Claude Code，依序執行：
/speckit.constitution    # 定義專案規範
/speckit.specify         # 定義第一個功能需求
/speckit.plan            # 制定技術計劃
/speckit.tasks           # 生成任務清單
/speckit.implement       # 開始實作
```

---

## 參考資源

- [Spec-Kit GitHub Repository](https://github.com/github/spec-kit)
- [Spec-Driven Development 概念](https://github.com/github/spec-kit#spec-driven-development)
