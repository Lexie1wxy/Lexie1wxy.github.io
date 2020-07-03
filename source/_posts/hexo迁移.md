---
title: hexo迁移
date: 2020-07-02 18:10:51
tags: [hexo]
categories: 
- 博客
typora-root-url: ../_posts
---

#### 怎么把环境文件托管到github

1. github创建hexo分支，setting——branches——设置hexo为默认分支，切换到hexo分支，`git clone -b hexo 项目git地址 `克隆仓库到本地

2. 此时本地会多出一个`username.github.io`文件夹，命令行`cd`进去，删除除了`.git`以外的所有文件夹

3. 把之前我们写的除了`.deploy_git`以外的所有博客源文件全部复制过来。这里应该说一句，复制过来的源文件应该有一个`.gitignore`，用来忽略一些不需要的文件，如果没有的话，自己新建一个，在里面写上如下，表示这些类型文件不需要git：

   ```text
   .DS_Store
   Thumbs.db
   db.json
   *.log
   node_modules/
   public/
   .deploy*/
   ```

   

   作者：直上云霄
   链接：https://www.zhihu.com/question/21193762/answer/489124966
   来源：知乎
   著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

4. 命令行`git add -A`把工作区的变化（包括已删除的文件）提交到暂存区（ps:`git add .`提交的变化不包括已删除的文件）。

5. 命令行`git commit -m "some description"`提交。

6. 命令行`git push origin hexo`推送到远程hexo分支。此时刷下github，如果正常操作，hexo分支应该已经被清空了。

7. 复制本地`username.github.io`文件夹中的`.git`文件夹到hexo项目根目录下。此时，hexo项目已经变成了和远程hexo分支关联的本地仓库了。而`username.github.io`文件夹的使命到此为止，你可以把它删掉，因为我们只是把它作为一个“中转站”的角色。以后每次发布新文章或修改网站样式文件时，`git add 然后 git commit -m "some description"  然后git push origin hexo`即可把环境文件推送到hexo分支。然后再`hexo g -d`发布网站并推送静态文件到master分支。

至此，hexo的环境文件已经全部托管在github的hexo分支了。

#### 新电脑中的环境搭建

这部分应该要简单一点，如果你已经搭建过一个hexo博客的话。

- 新电脑上安装node.js和git。不赘述。
- 安装hexo：`npm install -g hexo-cli`。
- clone远程仓库到本地 `git clone git@github.com:username/username.github.io.git`。
- 根据`packge.json`安装依赖`npm install`。
- 本地生成网站并开启博客服务器：`hexo g & hexo s`。如果一切正常，此时打开浏览器输入`http://localhost:4000/`已经可以看到博客正常运行了。

#### 在两台电脑上的同步操作

至此，迁移工作已完成，在两台电脑之间的同步操作如下：

- `git pull`从远程hexo分支拉取最新的环境文件到本地，可以理解为svn的更新操作。比如在公司写了博客，回家在电脑上也要写需要先执行这一步操作。
- 文章写完，要发布时，需要先提交环境文件，再发布文章。按以下顺序执行命令：`git add .`、`git commit -m "some descrption"`、`git push origin hexo`、`hexo g -d`。

```
  {% if theme.social %}
  ...
  {% endif %}


```

