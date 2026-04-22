# 博客本地运行与更新指南

您的博客环境已经在这台新电脑上配置成功！
所有代码存放于：`d:\projects\Blog\`
- **MyBlog** 文件夹是博客的源代码和 Hexo 配置文件。
- **SimonXiangD.github.io** 文件夹是部署在 GitHub Pages 上的静态页面仓库。

在这里向您介绍日常更新博客的常见步骤：

## 1. 编写新文章
打开终端或命令行，进入博客源码目录：
```powershell
cd d:\projects\Blog\MyBlog
```

然后使用以下命令生成一篇新文章（或者您可以直接在 `source/_posts` 目录下新建 Markdown 文件）：
```powershell
npx hexo new "我的新文章标题"
```
此时在 `source/_posts/` 下会生成一个同名的 [.md](file:///C:/Users/asdir/.gemini/antigravity/brain/02d22213-36c6-462a-89cd-9ee377814777/task.md) 文件，您可以使用任意编辑器（如 VSCode 或 Typora）打开并编写内容。

## 2. 本地预览（可选）
如果您希望在发布前预览文章效果，可以运行：
```powershell
npx hexo server
```
然后在浏览器中访问 `http://localhost:4000` 即可查看。预览完毕按 `Ctrl + C` 退出。

## 3. 生成与部署 (更新到 GitHub Pages)
当文章写好并确认无误后，使用以下命令生成静态文件并将其推送到您的 GitHub Pages 仓库：
```powershell
npx hexo clean
npx hexo generate
npx hexo deploy
```
或者简写为一条命令：
```powershell
npx hexo clean && npx hexo d -g
```

> [!NOTE]
> 如果您是在 PowerShell 中执行，可能会需要使用分号分隔命令：
> `npx hexo clean; npx hexo generate; npx hexo deploy`

> [!CAUTION]
> 部署 (deploy) 可能会提示您输入 GitHub 用户名和密码（或使用 Token / SSH 验证），这取决于您在本机设置的 Git 凭证。如果您还没登录 GitHub 的凭证，在弹出的窗口中登录即可。

## 4. 提交博客源码的改动 (备份 MyBlog 仓库)
Hexo deploy 只是把生成的公共页面发布到 `.github.io` 仓库，为了以后博客不丢失，建议您也定期将 `MyBlog` 目录下的博文源码变更提交到您的 MyBlog 仓库：

```powershell
git add .
git commit -m "update blog posts"
git push origin master
```

---
祝您在新电脑上写作愉快！如果还有其他配置需要调整，欢迎随时告诉我。
