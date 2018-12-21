title: Linux下 Hexo + GitHub 搭建个人博客

categories: Hexo

tags:
  - Hexo
  - GitHub

---
#### [Hexo](https://hexo.io/zh-cn/docs/index.html) 简介及搭建
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

---
##### 安装Hexo
安装 Hexo 相当简单。然而在安装前，您必须检查电脑中是否已安装下列应用程序：
*   [Git](http://git-scm.com/) -- 需要把本地的网页和文章等提交到 GitHub 上
*   [Node.js](http://nodejs.org/) -- Hexo 博客系统是基于 Node.js 编写的

---
##### 安装 Git

 `sudo apt-get install git-core`

安装成功
```
~ $ git --version
git version 2.7.4
```
---
##### 安装 Node.js

安装 Node.js 的最佳方式是使用 [nvm](https://github.com/creationix/nvm)。

> curl https://raw.github.com/creationix/nvm/v0.33.11/install.sh | sh
wget -qO- https://raw.github.com/creationix/nvm/v0.33.11/install.sh | sh

或者
> 手动安装： git clone http://github.com/creationix/nvm.git .nvm
cd .nvm
. install.sh

安装nvm完成后，`重启终端`并执行下列命令即可安装 Node.js
`nvm install stable`

安装成功
```
~ $ node -v
v11.3.0
```
---
##### 安装Hexo
使用 npm 安装 Hexo
> npm install -g hexo-cli

安装成功
```
~ $ hexo --version
hexo-cli: 1.1.0
```
---
##### 本地调式 Hexo
执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件

```
hexo init <folder>
cd <folder>
npm install # install node_modules
```
运行成功输出信息， 在浏览器中输入`http://localhost:4000`， 可以看到hexo页面。
```
$ hexo server
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
^C INFO  See you again
```
---
##### Github Pages托管
Github Pages服务可以给我们提供一个静态网页的托管，以便远程浏览我们的博客内容。

首先我们需要在本机生成一个`公钥`以便跟github建立安全连接，使用下面命令后，
一直enter下去。
>$ ssh-keygen -t rsa -C "email@domain.com"

这里的邮箱就是我们github **setting** 里面的邮箱，随后复制公钥内容：

>cat ~/.ssh/id_rsa.pub

复制后，登陆github，进入Settings->SSH and GPG keys->New SSH key->粘贴

随后进入系统测试连接是否成功：

>ssh -T git@github.com

根据提示输入yes，如果成功建立连接就可以进行接下来的操作了。

接下来我们使用我们需要在github上创建一个仓库repository，注意仓库名称必须为 [`github_user`].github.io (**github_user 是你github的用户名, 这点非常重要**)。

---
##### Hexo 与 GitHub Pages关联
* 配置 Deployment

在_config.yml文件中，找到Deployment文件，然后按照如下修改：（注意冒号后面记得空一格！）
```
# Deployment

## Docs: https://hexo.io/docs/deployment.html

deploy:

type: git

repo: git@github.com:github_user/github_user.github.io.git

branch: master
```
* 本地文件提交到 GitHub Pages，三个步骤，当然可以在生成静态文件后本地查看（hexo s）。
```
# 删除旧的 public 文件
hexo clean

# 生成新的 public 文件
hexo generate(hexo g)

# 本地查看
# hexo s

# 开始部署
hexo deploye(hexo d)
```
在浏览器中输入https://github_user.github.io 就可以看到你的简单博客了。可能需要等待一段时间才能访问的。

期间出现改错误提示： `ERROR Deployer not found: git`, 需要安装一个扩展
> npm install hexo-deployer-git --save

大功告成了 ~~~ ^
<!-- more -->
