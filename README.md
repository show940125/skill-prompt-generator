# Skill Prompt Generator - 基於 Skills 的智慧提示詞生成系統

**一個 Claude Code Skills 專案**，透過 12 個專業領域 Skills，基於 Universal Elements Library（1140+ 元素）生成高品質 AI 圖像提示詞。

## 🎯 專案定位

**這不是一個普通的 Python 工具，而是一個完整的 Skills 系統：**

- 🎨 **Skills 優先**：使用者透過呼叫 Skills 生成提示詞，不直接呼叫 Python
- 🧠 **智慧路由**：自動識別領域（人像/藝術/設計/產品/影片），呼叫對應專家
- 📦 **12 個專業 Skills**：每個領域有獨立的專家 Skill
- 💾 **統一資料來源**：所有 Skills 共用 Universal Elements Library（1140+ 元素）

## ✨ 核心特性

### 🎯 Skills 系統（核心）
- **12 個專業領域 Skills**：intelligent-prompt-generator, art-master, design-master, product-master, video-master, universal-learner 等
- **智慧領域路由**：自動識別使用者需求，呼叫對應專家
- **模組化架構**：每個 Skill 獨立工作，協同配合

### 🧠 智慧能力
- **語意理解**：區分主體/風格/氛圍
- **常識推理**：自動推斷合理屬性（如人種 → 眼睛顏色）
- **一致性檢查**：自動偵測並修正邏輯衝突
- **框架驅動**：基於 `prompt_framework.yaml` 結構化生成

### 📦 雙軌制系統
- **元素級生成**：從 1140+ 個元素中智慧選擇組合
- **模板級生成**：完整設計系統模板（如 Apple PPT 模板）

### 📦 支援領域
- 📷 **portrait** - 人像攝影（502 個元素）
- 🎨 **design** - 平面設計（80 個元素）
- 🏠 **interior** - 室內設計
- 📦 **product** - 產品攝影
- 🎭 **art** - 藝術風格
- 🎬 **video** - 影片生成
- 📸 **common** - 通用攝影技術（205 個元素）

## 📦 安裝

### 前置要求

- **Claude Code** - 需要安裝 Claude Code CLI
- **Python 3.8+** - 用於執行底層引擎
- **Git** - 用於複製專案（可選）

### 安裝步驟

#### 方式 1：複製到本地（推薦）

```bash
# 1. 複製專案
git clone https://github.com/huangserva/skill-prompt-generator.git

# 2. 進入專案目錄
cd skill-prompt-generator

# 3. 安裝 Python 依賴
pip install -r requirements.txt
```

**重要**：複製後，`.claude/skills/` 下的 12 個 Skills 會自動被 Claude Code 識別。

#### 方式 2：下載 ZIP

1. 造訪 https://github.com/huangserva/skill-prompt-generator
2. 點選 "Code" → "Download ZIP"
3. 解壓縮到任意目錄
4. 在該目錄下執行 `pip install -r requirements.txt`

### 驗證安裝

在 Claude Code 中測試：

```
# 測試人像生成 skill
生成電影級的亞洲女性

# 測試設計 skill
生成 Bento Grid 海報
```

如果 Claude Code 能正確呼叫 Skills 並生成提示詞，說明安裝成功。

---

## 🚀 快速開始

### 方式 1：透過 Skills 使用（推薦）⭐

**這是主要使用方式** - 在 Claude Code 中直接呼叫 Skills：

```
# 人像攝影
生成電影級的亞洲女性，張藝謀電影風格

# 平面設計
生成 Bento Grid 玻璃態海報

# 藝術繪畫
生成中國水墨畫山水

# 產品攝影
生成奢華手錶產品攝影
```

Claude Code 會自動：
1. 識別領域（人像/設計/藝術/產品）
2. 呼叫對應的專家 Skill
3. 回傳完美的提示詞

### 方式 2：直接呼叫 Python 引擎（開發/除錯）

如果你想直接呼叫底層引擎：

```bash
# 安裝依賴
pip install -r requirements.txt
```

```python
from intelligent_generator import IntelligentGenerator

gen = IntelligentGenerator()

# 生成人像提示詞
prompt = gen.generate_from_intent({
    'subject': {
        'gender': 'female',
        'ethnicity': 'East_Asian',
        'age_range': 'young_adult'
    },
    'styling': {
        'makeup': 'k_beauty'
    },
    'lighting': {
        'lighting_type': 'natural'
    }
})

print(prompt)
gen.close()
```

**注意**：直接呼叫 Python 引擎主要用於開發和除錯，日常使用建議透過 Skills。

## 📖 專案結構

```
.
├── .claude/                       # ⭐ Skills 系統（核心）
│   ├── CLAUDE.md                  # 專案規則和 Skill 路由指南
│   └── skills/                    # 12 個專業領域 Skills
│       ├── intelligent-prompt-generator/  # 人像提示詞專家
│       ├── art-master/            # 藝術風格專家
│       ├── design-master/         # 平面設計專家
│       ├── product-master/        # 產品攝影專家
│       ├── video-master/          # 影片生成專家
│       ├── universal-learner/     # 學習系統
│       ├── prompt-analyzer/       # 提示詞分析
│       ├── prompt-extractor/      # 元素擷取
│       ├── prompt-generator/      # 通用生成器
│       ├── prompt-master/         # 主控調度
│       ├── prompt-xray/           # X-Ray 分析
│       └── domain-classifier/     # 領域分類
│
├── intelligent_generator.py       # Python 引擎：核心生成
├── framework_loader.py            # Python 引擎：框架載入
├── element_db.py                  # Python 引擎：資料庫操作
├── prompt_framework.yaml          # 人像框架定義
│
├── extracted_results/
│   └── elements.db                # Universal Elements Library (1140+ 元素)
│
├── requirements.txt               # Python 依賴
└── README.md                      # 專案文件
```

**架構說明**：
- **使用者層**：透過 Claude Code 呼叫 Skills
- **Skills 層**：12 個專業領域專家（.claude/skills/）
- **引擎層**：Python 引擎支援 Skills 執行
- **資料層**：Universal Elements Library（1140+ 元素）

## 🎨 使用示例

### 示例 1：人像攝影（intelligent-prompt-generator skill）

**使用者請求**：
```
生成電影級的亞洲女性，張藝謀電影風格
```

**Skill 自動處理**：
- 識別：人像攝影領域
- 呼叫：intelligent-prompt-generator skill
- 生成：電影級人像提示詞，包含戲劇性光影

**輸出提示詞**：
```
Cinematic portrait of young East Asian woman, dramatic lighting with rim light
and chiaroscuro effect, Zhang Yimou's signature color palette with rich reds
and golds, 85mm lens, shallow depth of field, film grain texture...
```

### 示例 2：平面設計（design-master skill）

**使用者請求**：
```
生成 Apple 風格 PPT 模板
```

**Skill 自動處理**：
- 識別：平面設計領域
- 呼叫：design-master skill
- 查詢：Apple 淡藍商務 PPT 模板（12 個元素完整系統）

**輸出**：完整模板系統，包括背景、版面配置、配色、字體、視覺效果

### 示例 3：藝術繪畫（art-master skill）

**使用者請求**：
```
生成中國水墨畫山水
```

**Skill 自動處理**：
- 識別：藝術繪畫領域（無人物）
- 呼叫：art-master skill
- 生成：包含筆觸、留白、潑墨等技法的提示詞

### 示例 4：產品攝影（product-master skill）

**使用者請求**：
```
生成奢華手錶產品攝影
```

**Skill 自動處理**：
- 識別：產品攝影領域
- 呼叫：product-master skill
- 生成：商業級產品攝影提示詞

## 🛠️ 核心功能

### 1. 元素庫系統
- **1140+ 個可重複使用元素**
- 7 大領域分類
- 可重複使用性評分（1-10）
- SQLite 資料庫儲存

### 2. 模板系統
- 完整設計系統保存
- 包含設計理念、使用指南
- 元素結構化組織
- 支援 PPT、UI、品牌 VI 等

### 3. 智慧生成
- 框架驅動（`prompt_framework.yaml`）
- 語意匹配和推理
- 一致性檢查
- 自動衝突解決

### 4. 學習系統
- 從新提示詞中擷取元素
- 自動領域分類
- 可重複使用性評分
- 持續累積知識

## 📊 資料庫統計

- **總元素數**: 1140+
- **Portrait 領域**: 502 個（人像專用）
- **Design 領域**: 80 個（平面設計）
- **Common 領域**: 205 個（通用技術）
- **模板數**: 1 個（Apple 淡藍商務 PPT）

## 🔧 配置

### prompt_framework.yaml

定義人像提示詞的完整框架：
- 7 大類：subject, facial, styling, expression, lighting, scene, technical
- 欄位到資料庫的對應
- 依賴規則（如 era=ancient → makeup=traditional）
- 驗證規則

## 📝 開發指南

### 新增新元素

```python
from element_db import ElementDatabase

db = ElementDatabase()
db.add_element({
    'element_id': 'portrait_expressions_010',
    'domain_id': 'portrait',
    'category_id': 'expressions',
    'name': 'serene_smile',
    'chinese_name': '寧靜微笑',
    'ai_prompt_template': 'serene gentle smile...',
    'keywords': '["serene", "gentle", "peaceful"]',
    'reusability_score': 8.5
})
```

### 建立新模板

```python
template = {
    'template_id': 'template_xxx',
    'name': 'Template Name',
    'chinese_name': '模板中文名',
    'category': 'ppt_design',
    'element_ids': ['elem1', 'elem2', ...],
    'element_structure': {
        'backgrounds': ['elem1'],
        'layouts': ['elem2']
    },
    'design_philosophy': '設計理念...',
    'usage_scenarios': '使用場景...'
}
```

## 🤝 貢獻

歡迎提交 Issue 和 Pull Request！

## 📄 License

MIT License

## 🙏 致謝

- 基於 Claude Code Skills 系統
- Universal Elements Library 架構
- 框架驅動生成理念
