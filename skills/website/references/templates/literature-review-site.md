# 文献检索与综述写作网站模板

本模板用于创建“文献检索 + 可视化分析 + AI 辅助文献综述写作”类网站。

---

## 1. 项目定位

### 目标

帮助用户把分散的文献检索结果统一管理到一个可视化页面中，并基于真实文献材料，通过 OpenAI 兼容第三方接口辅助生成文献综述草稿。

### 典型用户

- 本科生、研究生
- 毕设/论文写作者
- 科研助理
- 需要整理行业研究资料的人
- 需要快速梳理研究现状的人

### 核心价值

- 用关键词和年限快速筛选文献
- 把检索到的文献统一汇总到一个页面
- 用图表查看年份趋势、关键词分布、来源分布
- 选择重点文献加入素材库
- 调用 OpenAI 兼容接口辅助生成综述草稿

---

## 2. 核心功能

## 2.1 检索条件区

必须包含：

| 字段 | 说明 |
|---|---|
| 关键词 | 支持输入一个或多个关键词 |
| 起始年份 | 例如 2020 |
| 结束年份 | 例如 2026 |
| 快捷年限 | 近 3 年 / 近 5 年 / 近 10 年 |
| 文献来源 | OpenAlex / Crossref / Semantic Scholar / 用户导入 |
| 文献类型 | 期刊 / 会议 / 学位论文 / 图书 / 全部 |
| 语言 | 中文 / 英文 / 全部 |

推荐提示语：

```text
请输入关键词，如：工程项目风险管理、巡检机器人、深度学习
```

---

## 2.2 文献统一展示区

检索结果要统一展示在一个可视化页面中，而不是分散在多个地方。

每条文献至少展示：

- 标题
- 作者
- 年份
- 来源
- DOI 或链接
- 摘要
- 关键词
- 相关度
- 是否已加入素材库

推荐操作：

- 查看详情
- 加入素材库
- 复制引用
- 标记重点
- 删除/隐藏

---

## 2.3 可视化分析区

推荐图表：

| 图表 | 用途 |
|---|---|
| 年份趋势图 | 查看某方向近几年研究热度 |
| 关键词分布图 | 找出研究热点 |
| 来源分布图 | 看主要期刊、会议或数据库来源 |
| 文献类型统计 | 区分期刊、会议、学位论文等 |
| 已选文献统计 | 了解综述素材覆盖情况 |

推荐技术：

- Recharts：简单、适合 React/Next.js
- ECharts：图表能力更强
- shadcn/ui Card：做统计卡片
- shadcn/ui Table：做文献表格

---

## 2.4 综述素材库

用户不应该把所有检索结果都交给 AI，而是先选择重要文献。

素材库字段建议：

```ts
type LiteratureNote = {
  paperId: string
  theme?: string
  keyPoint?: string
  method?: string
  conclusion?: string
  limitation?: string
  quote?: string
}
```

素材库功能：

- 已选文献列表
- 按主题分组
- 添加阅读笔记
- 摘录核心观点
- 标记研究方法、研究结论、研究不足

---

## 2.5 底部 AI 综述生成区

页面底部加入 AI 写作区，用于调用 OpenAI 兼容第三方接口。

### UI 结构

建议放在页面底部，或做成右侧固定抽屉。

包含：

- 综述类型选择
- 写作语言选择
- 引用格式选择
- 字数要求
- 额外要求输入框
- 生成按钮
- 结果预览区
- 复制 Markdown 按钮

### 综述类型

可选：

- 研究现状
- 研究热点
- 研究不足
- 发展趋势
- 国内外研究综述
- 完整文献综述草稿

### 接口配置

不要把 API Key 写死在前端。

推荐环境变量：

```env
OPENAI_BASE_URL=https://api.example.com/v1
OPENAI_API_KEY=your_api_key_here
OPENAI_MODEL=gpt-4o-mini
```

推荐接口：

```text
POST /api/literature-review
```

请求示例：

```json
{
  "papers": [
    {
      "title": "文献标题",
      "authors": ["作者1", "作者2"],
      "year": 2024,
      "abstract": "摘要内容",
      "source": "期刊或会议",
      "doi": "10.xxxx/xxxx"
    }
  ],
  "reviewType": "研究现状",
  "requirements": "请按学术论文风格写作，保留引用标记",
  "language": "zh",
  "citationStyle": "GB/T 7714"
}
```

---

## 3. 页面结构建议

```text
页面顶部
├── 项目名称
├── 导入文献
├── 接口设置
└── 导出结果

检索区
├── 关键词输入
├── 起始年份
├── 结束年份
├── 近3年 / 近5年 / 近10年
├── 来源筛选
└── 检索按钮

统计概览
├── 总文献数
├── 年份范围
├── 核心关键词数
└── 已选文献数

可视化区
├── 年份趋势图
├── 关键词分布图
└── 来源分布图

文献列表区
├── 标题
├── 作者
├── 年份
├── 摘要
├── 相关度
└── 加入素材库

素材库区
├── 已选文献
├── 主题分组
└── 阅读笔记

底部 AI 综述区
├── 综述类型
├── 写作要求
├── 调用接口生成
└── Markdown 结果
```

---

## 4. 数据结构建议

```ts
type Paper = {
  id: string
  title: string
  authors: string[]
  year: number
  source?: string
  abstract?: string
  keywords?: string[]
  doi?: string
  url?: string
  citationCount?: number
  relevanceScore?: number
  selected?: boolean
}

type LiteratureSearchFilters = {
  query: string
  startYear?: number
  endYear?: number
  recentYears?: 3 | 5 | 10
  source?: string
  documentType?: "journal" | "conference" | "thesis" | "book" | "all"
  language?: "zh" | "en" | "all"
}

type ReviewGenerationRequest = {
  papers: Paper[]
  reviewType: "研究现状" | "研究热点" | "研究不足" | "发展趋势" | "完整文献综述"
  requirements?: string
  language: "zh" | "en"
  citationStyle: "GB/T 7714" | "APA" | "MLA" | "IEEE"
}
```

---

## 5. 安全与合规要求

必须提醒用户：

- AI 生成内容只能作为草稿
- 不要直接提交未经核对的 AI 综述
- 不允许编造文献
- 不允许编造 DOI、作者、期刊、年份
- 引用必须来自真实检索或用户导入的文献
- API Key 不要写死在前端
- `.env.local` 不要提交到 GitHub

---

## 6. 推荐技术栈

| 模块 | 推荐 |
|---|---|
| 前端 | Next.js + TypeScript |
| 样式 | Tailwind CSS |
| UI 组件 | shadcn/ui |
| 图标 | lucide-react |
| 图表 | Recharts 或 ECharts |
| 表格 | TanStack Table 或 shadcn table |
| 状态管理 | Zustand 或 React state |
| AI 接口 | OpenAI SDK 或 fetch 调用 OpenAI 兼容接口 |
| 部署 | Vercel |

---

## 7. AI 生成综述提示词模板

```text
你是一名严谨的学术写作助手。

请只基于我提供的文献材料，辅助生成文献综述草稿。

要求：
1. 不要编造不存在的文献。
2. 不要编造 DOI、作者、期刊、年份。
3. 引用只能来自我提供的文献。
4. 使用学术论文风格，但语言要清楚。
5. 按主题归纳，而不是逐篇罗列。
6. 明确指出已有研究的主要方向、方法、结论和不足。
7. 输出 Markdown 格式。

综述类型：
【研究现状 / 研究热点 / 研究不足 / 发展趋势 / 完整文献综述】

引用格式：
【GB/T 7714 / APA / MLA / IEEE】

文献材料：
【粘贴文献列表】
```
