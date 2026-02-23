---
title: GithubPage + Hexo方案搭建个人博客
date: 2026-02-21 22:25:29
---
第一次搭建个人博客成功，记录一下过程。

我使用的是macos系统，采用GithubPage + Hexo的方案，好处是很好部署，而且完全免费，不需要购买域名和服务器；缺点也很明显，静态网页更新麻烦一些，需要每次在本地修改好后，通过hexo命令生成静态网页并推送到GithubPage，同时还要维护一个项目仓库。也就是说需要在github创建**一个GithubPage仓库和一个博客项目仓库**。
<br>

# 第一步：创建GithubPage仓库
首先你需要有一个github账号，然后创建一个新的仓库，这里要注意仓库的名字必须是**你的github用户名.github.io**，并勾选**Add README**。

![创建GithubPage仓库](/image/Snipaste_2026-02-21_23-40-18.png)

之后点击*create repository*按钮完成GithubPage仓库的创建。

进入仓库主页，点击*settings*，点击侧边栏的*pages*就可以看到你刚创建的博客域名了。

![pages页面](/image/Snipaste_2026-02-21_23-56-22.png)
<br>

# 第二步：部署Hexo
Hexo是一个基于Node.js的静态博客框架，在安装Hexo之前你需要先安装Git和Node.js，我使用HomeBrew安装，只需要输入两个命令，非常方便。这里不做过多赘述。

安装完成后，你需要在本地创建一个新的文件夹，用来存放博客项目。进入文件夹，右键文件目录打开终端。

输入命令初始化一个Hexo项目

```bash
hexo init
```

之后终端会输出*Start blogging with Hexo!*，检查项目目录，应该会有一些文件和文件夹，此时说明创建成功。
进入项目根目录，打开<em>_config.yml</em>文件，在最底部添加以下内容：
```yml
deploy:
  type: git
  repo: git@github.com:***/***.github.io.git
  branch: main
```
> PS: repo是项目的SSH key，branch是项目的分支

修改完毕后保存并退出。

进入终端，输入命令
```bash
hexo generate
hexo deploy
```
*generate*完成后可以看到根目录多了一个*public*文件夹，里面存放了生成的静态网页文件；*deploy*会把本地*public*文件夹中的文件推送到GithubPage仓库上。

完成后就可以在浏览器中输入你的博客域名，访问到你的个人博客了。
<br>

# 第三步：设置主题
Hexo提供了很多主题，让你的博客变得更个性化，更好看。你可以在[官方网站](https://hexo.io/themes/)上预览并选择一个你喜欢的主题。

![主题预览](/image/Snipaste_2026-02-23_22-23-58.png)

第一个框是主题的名字，点击可以进入该主题的github仓库，查看该主题的详细信息；
第二个框是该主题的预览网页，可以查看实际效果。

选择你喜欢的主题后，进入该主题的github，将项目克隆到本地博客项目的themes文件夹下。

通常作者都会写出主题的初始化方法，以及如何自定义你的主题，根据教程一步步来定制属于自己的博客。
>PS: 建议fork项目以便后续同步项目的更新、自定义修改。

<br>

# 第四步：创建项目仓库
现在你的博客已经搭建完成了，为了确保博客项目的后续管理，你需要创建一个新的仓库，用来存放博客项目的代码。

创建方式和[第一步](#第一步：创建GithubPage仓库)类似，不同的是仓库的名字可以任意取，记住别勾选**Add README**。

回到本地博客项目的根目录，开始创建git仓库，打开终端输入以下命令：
```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:***/***.git
git push -u origin main
```
> PS: 倒数第二行的命令复制项目的SSH key。

到这里，项目仓库就创建完成了。
<br>

# 第五步：创建一篇博客
接下来开始写你的第一篇博客吧！

回到本地博客项目的根目录，打开终端，输入命令创建新的博客
```bash
hexo new "我的第一篇博客"
```
> PS: 命令中的双引号可以省略，但是如果博客标题中包含空格或一些特殊符号，就必须要加上双引号。

创建完成后，在*source/_posts*中打开新创建的***我的第一篇博客.md***文件，开始撰写你的博客，这期间你可以通过
```bash
hexo server
```
启动本地服务器，在浏览器中输入 http://localhost:4000 预览你的博客，确保博客内容符合你的预期。

完成后，通过以下命令将文件部署到你的博客：
```bash
hexo clean
hexo generate
hexo deploy
```
<br>

# 参考链接
Hexo官方文档：
<https://hexo.io/zh-cn/docs/>
更详细的搭建教程可参考这位博主：
<https://oceanwang.top/personal-website-1/>
我使用的Hexo主题：
<https://github.com/fi3ework/hexo-theme-archer>