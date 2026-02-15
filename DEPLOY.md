# CSAPP GitBook 部署指南

本指南介绍如何将 CSAPP 电子书部署到 Vercel 平台。

## 项目结构

```
├── CSAPP_OCR_FINAL/       # 原始 OCR 内容（16个分块）
│   ├── chunk_0001_0050/   # 第1-50页
│   ├── chunk_0051_0100/   # 第51-100页
│   └── ...
├── SUMMARY.md             # GitBook 目录结构
├── README.md              # 首页内容
├── book.json              # GitBook 配置
├── package.json           # 依赖管理
└── vercel.json            # Vercel 部署配置
```

## 本地开发

### 1. 安装依赖

```bash
npm install
```

### 2. 本地预览

```bash
npm run dev
```

访问 `http://localhost:4000` 即可预览电子书。

### 3. 构建

```bash
npm run build
```

构建后的静态文件位于 `_book/` 目录。

## 部署到 Vercel

### 方法一：通过 Vercel 网站部署

1. 访问 [Vercel](https://vercel.com)
2. 点击 **Add New Project**
3. 导入此 GitHub 仓库
4. Vercel 会自动检测配置：
   - Framework Preset: **Other**
   - Build Command: `npm run build`
   - Output Directory: `_book`
5. 点击 **Deploy**

### 方法二：通过 Vercel CLI 部署

```bash
# 安装 Vercel CLI
npm i -g vercel

# 登录
vercel login

# 部署
vercel --prod
```

## 配置说明

### book.json

- 禁用了 `search` 和 `lunr` 插件（因为内容量大会导致构建失败）
- 启用了 `fontsettings` 插件（允许调整字体大小）
- 使用中文界面 (`zh-hans`)

### vercel.json

```json
{
  "framework": null,
  "buildCommand": "npm run build",
  "outputDirectory": "_book"
}
```

## 自动部署

每次推送到 `main` 分支，Vercel 会自动触发重新部署。

## 注意事项

1. **构建时间**: 由于内容量较大，首次构建可能需要 1-2 分钟
2. **搜索功能**: 由于禁用了搜索插件，可使用浏览器的内置搜索功能（Ctrl+F）
3. **图片**: 所有图片都已包含在 OCR 内容中，会自动复制到构建输出

## 故障排除

### 构建失败

如果遇到 "Maximum call stack size exceeded" 错误：
- 确保 `book.json` 中已禁用 `search` 和 `lunr` 插件
- 检查 Node.js 版本（需要 >=18）

### 图片无法显示

- 确保图片路径使用相对路径
- 检查图片文件是否存在于对应的 chunk 目录中

## 更新内容

1. 修改 SUMMARY.md 或内容文件
2. 提交并推送到 GitHub
3. Vercel 会自动重新部署

---

如有问题，请在 GitHub 仓库中提交 Issue。
