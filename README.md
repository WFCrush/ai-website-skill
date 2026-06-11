# ai-website-skill

AI 建站与部署工作流 skill，用于帮助小白按专业流程创建、优化和部署网站项目。

本项目参考成熟 skill 包结构组织，核心内容全部采用 Markdown 文档格式，适配 Claude Code / OpenClaw 等支持 skill 的 AI 编程工具。

## 适用场景

- 从零创建企业官网、SaaS 官网、作品集、Landing Page
- 给已有网站做 UI 美化和专业化改造
- 制定网站 UI 设计规范
- 设计首页结构和转化文案
- 使用 Next.js / Tailwind CSS / shadcn/ui 实现页面
- 根据截图进行 UI 审查和迭代优化
- 指导部署到 Vercel、Netlify、Cloudflare Pages 等平台
- 创建文献检索与综述写作类网站：支持文献年限筛选、关键词检索、可视化文献页面和 OpenAI 兼容接口辅助生成综述草稿

## Skill 名称

```text
website
```

建议调用方式：

```text
/website
```

也可以使用：

```text
/建站
/网站
```

或明确说明：

```text
请使用 website skill 帮我创建一个专业官网
```

## 目录结构

```text
.
├── CLAUDE.md
├── README.md
├── LICENSE
├── .claude-plugin
│   └── marketplace.json
└── skills
    └── website
        ├── SKILL.md
        └── references
            └── templates
                ├── website-workflow.md
                ├── prompt-templates.md
                ├── ui-quality-checklist.md
                ├── deployment-checklist.md
                └── literature-review-site.md
```

## 核心流程

website skill 会按照以下流程工作：

1. 需求分析
2. 视觉风格定位
3. UI 设计规范
4. 首页结构与文案
5. 前端开发
6. 截图审查优化
7. 部署上线

## 设计原则

- 不要一上来写代码，先明确需求、风格和 UI 规范
- 不让 AI 自由发挥，用流程和规范约束结果
- 默认追求现代、简洁、高级、清晰、有留白
- 默认避免廉价渐变、过多阴影、花哨动画、颜色混乱、模板感
- 对小白友好，不默认用户懂 Git、命令行、服务器或前端工程化

## 推荐技术栈

- Next.js
- TypeScript
- Tailwind CSS
- shadcn/ui
- lucide-react
- Vercel

## 参考文档

| 文件 | 用途 |
|---|---|
| `skills/website/SKILL.md` | skill 主入口和完整工作规则 |
| `skills/website/references/templates/website-workflow.md` | AI 建站完整工作流 |
| `skills/website/references/templates/prompt-templates.md` | 可复制的建站提示词模板 |
| `skills/website/references/templates/ui-quality-checklist.md` | UI 质量审查清单 |
| `skills/website/references/templates/deployment-checklist.md` | 部署上线检查清单 |
| `skills/website/references/templates/literature-review-site.md` | 文献检索、可视化分析与 AI 综述写作网站专项模板 |

## License

MIT
