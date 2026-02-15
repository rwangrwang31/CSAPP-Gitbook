# 发布与部署（GitHub + Vercel）

## 1. 推送到 GitHub

在项目根目录执行：

```bash
git init
git add .
git commit -m "init: gitbook(honkit) + vercel config"
git branch -M main
git remote add origin <你的仓库地址>
git push -u origin main
```

## 2. 本地预览（可选）

```bash
npm install
npm run dev
```

默认访问 `http://localhost:4000`。

## 3. Vercel 部署

1. 打开 Vercel，选择 **Add New Project**。
2. 导入该 GitHub 仓库。
3. 保持默认（仓库内已有 `vercel.json`）：
   - Build Command: `npm run build`
   - Output Directory: `_book`
4. 点击 **Deploy**。

后续每次 push 到 `main`，Vercel 会自动重新部署。
