# 网站部署检查清单

用于指导小白把网站部署上线，优先适配 Next.js / React / Vue / 静态站点。

---

## 1. 先判断项目类型

| 项目类型 | 推荐平台 |
|---|---|
| Next.js | Vercel |
| React / Vite | Netlify / Vercel / Cloudflare Pages |
| Vue / Vite | Netlify / Vercel / Cloudflare Pages |
| 静态 HTML | Netlify / Cloudflare Pages |
| 有后端 API | Railway / Render / Fly.io / VPS |
| 需要数据库 | Supabase / Neon / PlanetScale / Railway |

---

## 2. 部署前本地检查

必须确认：

- 项目可以本地启动
- 项目可以成功构建
- 没有 TypeScript 报错
- 没有 ESLint 阻塞错误
- 图片路径正确
- 环境变量已整理
- `.env` 没有上传敏感信息
- Git 仓库状态清楚

---

## 3. 常见命令

### Next.js

```bash
npm install
npm run dev
npm run build
npm run start
```

### Vite React / Vue

```bash
npm install
npm run dev
npm run build
npm run preview
```

---

## 4. GitHub 上传流程

适合小白的解释：

1. 在 GitHub 新建一个仓库
2. 在本地项目目录打开终端
3. 初始化 Git
4. 添加文件
5. 提交代码
6. 连接远程仓库
7. 推送到 GitHub

常见命令：

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <你的仓库地址>
git push -u origin main
```

如果用户不懂 Git，要逐步解释每条命令。

---

## 5. Vercel 部署流程

推荐用于 Next.js。

1. 打开 https://vercel.com
2. 使用 GitHub 登录
3. 点击 Add New Project
4. 选择 GitHub 仓库
5. 检查 Framework Preset 是否识别为 Next.js
6. 检查 Build Command
7. 检查 Output Directory
8. 配置环境变量
9. 点击 Deploy
10. 部署完成后打开预览链接检查

---

## 6. Netlify 部署流程

推荐用于静态站点、React、Vue。

1. 打开 https://netlify.com
2. 使用 GitHub 登录
3. Add new site
4. Import from Git
5. 选择仓库
6. 设置构建命令
7. 设置发布目录
8. 配置环境变量
9. Deploy

常见配置：

| 项目 | Build command | Publish directory |
|---|---|---|
| Vite | npm run build | dist |
| React CRA | npm run build | build |
| 静态 HTML | 留空或自定义 | 项目根目录 |

---

## 7. Cloudflare Pages 部署流程

适合静态站点、全球访问速度要求高的项目。

1. 打开 Cloudflare Dashboard
2. Workers & Pages
3. Create application
4. Pages
5. Connect to Git
6. 选择仓库
7. 设置构建命令和输出目录
8. 保存并部署

---

## 8. 环境变量检查

常见环境变量：

- API 地址
- 数据库连接字符串
- Supabase URL / Key
- Stripe Key
- OAuth Client ID / Secret
- OpenAI / Anthropic API Key

注意：

- `.env.local` 不要上传 GitHub
- 部署平台需要单独配置环境变量
- 变量名必须和代码中读取的一致

---

## 9. 常见部署失败原因

| 问题 | 原因 | 解决 |
|---|---|---|
| build 失败 | TypeScript / ESLint 错误 | 先本地运行 build 修复 |
| 页面空白 | 路由或资源路径错误 | 检查控制台和网络请求 |
| API 报错 | 环境变量没配置 | 在部署平台添加环境变量 |
| 图片不显示 | 图片路径错误或远程域名未配置 | 检查 next.config.js |
| 404 | 路由配置或输出目录错误 | 检查平台配置 |
| 本地能跑线上不行 | 依赖版本或环境变量差异 | 对比 Node 版本和 env |

---

## 10. 绑定域名

通用步骤：

1. 在部署平台添加自定义域名
2. 到域名服务商后台修改 DNS
3. 添加平台要求的 CNAME 或 A 记录
4. 等待 DNS 生效
5. 检查 HTTPS 证书是否自动签发

---

## 11. 部署完成后检查

- 首页能打开
- 手机端能打开
- 按钮可点击
- 表单可提交
- 图片正常显示
- 控制台没有明显错误
- 页面加载速度可接受
- SEO 标题和描述不为空

---

## 12. 小白解释原则

部署时不要只给命令，要解释：

- 这一步做什么
- 为什么要做
- 成功后应该看到什么
- 如果失败，把报错截图/文字发给我
