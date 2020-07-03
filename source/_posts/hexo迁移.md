---
title: hexo迁移
date: 2020-07-02 18:10:51
tags: [hexo]
categories: 
- 博客
typora-root-url: ../_posts
---

#### 怎么把环境文件托管到github

1. github创建hexo分支，setting——branches——设置hexo为默认分支，切换到hexo分支，git clone仓库到本地

2. 此时本地会多出一个username.github.io文件夹，命令行cd进去，删除除了.git`以外的所有文件夹

3. 把之前我们写的除了  .deploy_git  以外的所有博客源文件全部复制过来。这里应该说一句，复制过来的源文件应该有一个  .gitignore ,用来忽略一些不需要的文件，如果没有的话，自己新建一个，在里面写上如下，表示这些类型文件不需要git：

   ```text
   .DS_Store
   Thumbs.db
   db.json
   *.log
   node_modules/
   public/
   .deploy*/
   ```

4. 命令行git add -A把工作区的变化（包括已删除的文件）提交到暂存区（ps:因为git add .提交的变化不包括已删除的文件）。

5. 命令行git commit -m "add branch"提交。

6. 命令行git push origin hexo推送到远程hexo分支。此时刷下github，如果正常操作，刷新可以知道hexo分支应该已经被清空了。

7. 复制本地username.github.io文件夹中.git文件夹到hexo项目根目录下。此时，hexo项目已经变成了和远程hexo分支关联的本地仓库了。

8. 而username.github.io文件夹的使命到此为止，你可以把它删掉，因为我们只是把它作为一个“中转站”的角色。

9. 以后每次发布新文章或修改网站样式文件时，git add 然后 git commit -m "description"  然后git push origin hexo即可把环境文件推送到hexo分支。然后再`hexo g -d发布网站并推送静态文件到master分支。

   每次发布代码：

   ```汇编
   git add .
   git commit –m "xxxx"
   git push origin hexo
   hexo g -d
   ```

至此，hexo的环境文件已经全部托管在github的hexo分支了。

#### 新电脑中的环境搭建

- 一样的，跟之前的环境搭建一样，

  - 安装git

  ```text
  sudo apt-get install git
  ```

  - 设置git全局邮箱和用户名

  ```text
  git config --global user.name "yourgithubname"
  git config --global user.email "yourgithubemail"
  ```

  - 设置ssh key

  ```text
  #命令行进入用户主目录
  ssh-keygen -t rsa -C "username@example.com"
  #输入邮箱后一路回车
  #找到该目录下.ssh文件夹，可以看到id_rsa（私钥）和id_rsa.pub（公钥），复制公钥
  #生成后去github上settings——>SSH and GPG keys,点击NEW SSH key然后title填个电脑名，把刚刚复制的粘贴到key中，点击add SHH key
  #验证是否成功
  ssh -T git@github.com
  ssh -T git@git.coding.net #(有coding平台的话)
  ```

  - 安装nodejs

  ```text
  sudo apt-get install nodejs
  sudo apt-get install npm
  ```

  - 安装hexo  

  ```text
  sudo npm install hexo-cli -g
  ```

  但是已经不需要初始化了

- clone远程仓库到本地

  ```
   git clone git@github.com:username/username.github.io.git
  ```

- 然后进入克隆到的文件夹：

  ```text
  cd xxx.github.io
  npm install
  npm install hexo-deployer-git --save
  ```

  生成，部署：

  ```text
  hexo g
  hexo d
  hexo s
  ```

- 如果一切正常，此时打开浏览器输入http://localhost:4000/已经可以看到博客正常运行了。

- 然后开始写新博客

  ```
  hexo n "博客名字"
  ```

- 写完了要记得源文件上传一下

  ```
  git add .
  git commit –m "xxxx"
  git push origin hexo
  hexo g -d
  ```

#### 在两台电脑上的同步操作

至此，迁移工作已完成，在两台电脑之间的同步操作如下：

- git pull从远程hexo分支拉取最新的环境文件到本地，可以理解为svn的更新操作。比如在公司写了博客，回家在电脑上也要写需要先执行这一步操作。
- 文章写完，要发布时，也需要先提交环境文件，再发布文章。按以下顺序执行命令：
- git add .、git commit -m "some descrption"、git push origin hexo、hexo g -d

```
//已经编辑过的电脑上，有clone文件夹了，就只用加个git pull
git pull
git add .
git commit –m "xxxx"
git push origin hexo
hexo g -d
```

