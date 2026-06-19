---
title: 从零搭建 Hugo + GitHub Pages 个人博客
date: 2026-06-19
draft: false
categories:
  - Tools
tags:
  - Hugo
  - GitHub
  - PaperMod
---
## 前言

一直想拥有一个自己的技术博客。

过去的学习笔记都记录在 Obsidian 中。

最近完成了 Hugo + GitHub Pages 博客的搭建，因此记录整个过程以及踩过的坑，希望能够帮助后来者少走弯路。

### 最终效果

博客地址：

[https://keyooooo.github.io/blog/](https://keyooooo.github.io/blog/)

技术栈：

- Hugo
- PaperMod
- GitHub Actions
- GitHub Pages

### 为什么选择 Hugo

#### Hugo 的优点

- 构建速度快
- 基于 Markdown 写作
- 免费部署
- SEO 友好
- 主题丰富

# 安装 Hugo

推荐在hugo官方GitHub下载，链接：[点这里！](https://github.com/gohugoio/hugo/releases)
推荐版本比较新的版本里的extended_withdeploy，因为未来可以把生成的网站直接部署到云存储（AWS S3、Google Cloud Storage 等。笔者这里下载的是hugo_extended_withdeploy_0.163.2_windows-amd64.zip，根据你自己的需求具体选择。

下载完成后解压hugo_extended_withdeploy_0.163.2_windows-amd64.zip，得到以下目录结构

```
└─hugo_extended_withdeploy_0.163.2_windows-amd64
    ├─hugo.exe
    ├─LICENSE
    └─README.md

```

先进入目录

```PowerShell
cd D:\你自己的存放位置\hugo_extended_withdeploy_0.163.2_windows-amd64
```

执行：

```PowerShell
.\hugo.exe version
```

如果看到类似：

```
hugo v0.163.2-xxxx windows/amd64
```

说明 Hugo 本身没问题。

然后加入环境变量（推荐）

否则以后每次都要：

```PowerShell
D:\Hugo\hugo_extended_withdeploy_0.163.2_windows-amd64\hugo.exe
```

方法：
window搜索 ***编辑系统环境变量*** ，点击环境变量
![编辑环境变量](images/hugo/env-path.png)

进入环境变量，找到用户变量的变量Path，双击Path编辑Path变量，点击新建，将刚才的
```text
D:\你自己的存放位置\hugo_extended_withdeploy_0.163.2_windows-amd64
```
粘贴到Path新建环境变量中，点击确定，然后再次点击环境变量整个窗口的确定

**新开**一个PowerShell窗口
执行
```PowerShell
hugo version
```
看到类似下面的内容就是配置环境变量配置成功了
```
hugo hugo v0.163.2...
```


# 创建 Hugo 站点

### 创建博客项目

找个你专门放项目的目录，例如：

```
D:\Blog
```

执行：

```PowerShell
mkdir D:\Blog
cd D:\Blog
hugo new site your_own_name
```

你会看到和得到：

```
Congratulations!Your new Hugo site was created
```

```
your_own_name
├── archetypes
├── assets
├── content
├── data
├── layouts
├── static
├── themes
└── hugo.toml
```

### 进入项目并执行初始化

```PowerShell
cd your_own_name
```

初始化Git

```PowerShell
git init
```

### 安装 PaperMod 主题

执行

```PowerShell
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### 配置 hugo.toml

打开D:\Blog\your_own_name\hugo.toml，删除原内容，替换成以下内容：

```
baseURL = "https://example.org/"
defaultContentLanguage = "zh-cn"
title = "your-title"
theme = "PaperMod"
```

先保持最简单。

### 创建第一篇文章

执行
```PowerShell
hugo new posts/hello-world.md
```
生成
```
content/posts/hello-world.md
```
编辑md文件
```Markdown
---  
title: "Hello Hugo"  
date: 2026-06-18  
draft: false  
---  
  
# 我的第一篇博客  
  
如果你看到这篇文章，  
  
说明 Hugo 已经运行成功了。  

```

### 本地预览

在：
```
D:\Blog\your_own_name
```
目录下执行：
```PowerShell
hugo server
```
如果配置正确会看到：
```
Start building sites …...Web Server is available at http://localhost:1313/
```
访问本地网站：
```
http://localhost:1313/
```
然后你就可以看到你的第一个博客网站啦

# 上传到 GitHub

### 在 GitHub 创建仓库

进入 GitHub，点击 New Repository。  
仓库配置如下：  
```text  
Repository name:  
blog  
  
Visibility:  
Public  
  
Add README:  
× 不勾选  
  
.gitignore:  
None  
  
License:  
None  
```  
创建完成后，会得到一个空仓库。  

---  
  
### 连接本地仓库  
  
进入 Hugo 项目目录：  
```powershell  
cd D:\Blog\your_own_name  
```  
添加远程仓库（请替换为自己的 GitHub 用户名）：  
```powershell  
git remote add origin https://github.com/your-github-username/blog.git  
```  
验证是否添加成功：  
```powershell  
git remote -v  
```  
如果看到类似输出：  
```text  
origin https://github.com/your-github-username/blog.git (fetch)  
origin https://github.com/your-github-username/blog.git (push)  
```  
说明远程仓库已经配置成功。  
  
---  

### 提交代码到本地仓库  
  
将项目文件加入 Git：  
```powershell  
git add .  
```  
创建第一次提交：  
```powershell  
git commit -m "Initial Hugo blog"  
```  
如果提交成功，会看到类似输出：  
```text  
[master (root-commit) xxxxxxx] Initial Hugo blog  
```  
  
---  
  
### 推送到 GitHub  
  
先查看当前分支名称：  
```powershell  
git branch  
```  
如果输出：  
```text  
* master  
```  
执行：  
```powershell  
git push -u origin master  
```  
如果输出：  
```text  
* main  
```  
执行：  
```powershell  
git push -u origin main  
```  
首次推送成功后，会看到类似输出：  
```text  
branch 'master' set up to track 'origin/master'  
```  
此时刷新 GitHub 页面，就可以看到 Hugo 项目已经上传成功。  
  
---  
  
### 关于 master 和 main  
  
不同 Git 版本默认分支名称可能不同：  
  
| 分支名 | 说明 |  
|---------|---------|  
| master | 旧版本 Git 默认分支 |  
| main | 新版本 Git 默认分支 |  
  
后续只需要使用当前仓库的默认分支即可，无需强制修改。
  
但此时仓库中的内容还只是代码，并不能通过网址访问。  
  
下一步，我们将配置 GitHub Pages 和 GitHub Actions，实现博客的自动部署。

# 配置 GitHub Pages 自动部署

首先我们需要修改hugo.toml文件，因为我们之前toml文件只是一个测试hugo能在本地跑起来而已。
编辑覆盖hugo.toml文件如下
```toml
#hugo.toml
baseURL = "https://your-github-username.github.io/blog/"
defaultContentLanguage = "zh-cn"
title = "your-title"
theme = "PaperMod"

[taxonomies]
tag = "tags"
category = "categories"

[[menu.main]]
identifier = "posts"
name = "文章"
url = "/posts/"
weight = 10

[[menu.main]]
identifier = "categories"
name = "分类"
url = "/categories/"
weight = 20

[[menu.main]]
identifier = "tags"
name = "标签"
url = "/tags/"
weight = 30

[[menu.main]]
identifier = "about"
name = "关于我"
url = "/about/"
weight = 40

[[menu.main]]
identifier = "links"
name = "友链"
url = "/links/"
weight = 50

[params]
ShowReadingTime = true
ShowCodeCopyButtons = true
ShowBreadCrumbs = true
ShowToc = true
```
编辑完后保存即可，然后执行一下：
```PowerShell
hugo server
```
访问：
```
http://localhost:1313
```
确认博客还能正常打开。

接下来创建GitHub Actions，目录：
```
D:\Blog\your-own-name
```
执行：
```PowerShell
mkdir .github
mkdir .github\workflows
ni .github/workflows/hugo.yml
```
编辑hugo.yml，一下是我的的yml文件内容，请根据你的版本更改hugo-version
```YAML
name: Deploy Hugo site to Pages

on:
  push:
    branches:
      - master
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: '你的版本号'
          extended: true

      - name: Build
        run: hugo

      - name: Setup Pages
        uses: actions/configure-pages@v5

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

      - name: Deploy
        id: deployment
        uses: actions/deploy-pages@v4
```

接下来我们提交配置
目录：
```
D:\Blog\your-own-name
```
执行：
```PowerShell
git add .
git commit -m "Add GitHub Pages workflow"
git push
```


开启 Pages：按下图在你的项目仓库里找到这个界面
![GitHub Pages 设置界面](images/hugo/pages-setting.png)
把Source从Deploy from a branch改成GitHub Actions
![切换 Source 为 GitHub Actions](images/hugo/pages-action.png)

进入Actions，你会看到
Deploy Hugo site to Pages正在运行。
等Actions部署完成，就可以访问博客。
成功后地址是：
```
https://your-github-username.github.io/blog/
```

## 添加 .gitignore

项目根目录创建：
```
.gitignore
```
.gitignore文件里的内容：
```gitignore
public/
resources/
.hugo_build.lock
```
然后：
```PowerShell
git rm -r --cached public
git rm --cached .hugo_build.lock
git add .
git commit -m "cleanup generated files"
git push
```
这样仓库会干净很多。

## 总结

至此，一个基于 Hugo、PaperMod、GitHub Actions 和 GitHub Pages 的个人博客就搭建完成了。

整个过程并不复杂，但中间仍然会遇到一些环境配置、路径以及部署相关的问题。

希望这篇文章能够帮助后来者少踩一些坑。

博客搭建只是开始，未来我会持续在这里记录。

希望多年以后回头看，这里已经积累了足够多值得分享的内容。