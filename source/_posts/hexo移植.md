---
title: hexo移植
date: 2019-10-08 17:16:36
categories: 生活
tags:
   -hexo
cover: https://i.loli.net/2019/10/07/iozjZ1pGvQTwAah.jpg
---

### hexo双部署步骤

### 一、安装Git和Node.js

官网下载

1. [安装Node.js](https://nodejs.org/en/)
2. [安装Git](https://git-scm.com/)

### 二、github新建分支

在**username.io**仓库下：

![](https://i.loli.net/2019/10/09/9ipCvYqr2e3gIxu.jpg)

分支名称任意，比如:hexo

### 三、设置分支为默认仓库

仓库->Settings->Branches->Default branch中将默认分支设为xxx，save保存。

![](http://image.huvjie.com/190219-03_img03.jpg)

### 四、clone到本地

本地新建一个文件夹用来管理博客，将分支克隆至本地。

```
git clone XXXXX.io
```

### 五、新电脑生成ssh key并添加至 gitHub

将新电脑生成的`ssh key`添加到`gitHub`账户上

1. `git config --global user.email "xxx@qq.com"` # 填写你github注册并且验证的邮箱；
2. `git config --global user.name "xxxx"` # github 用户名；
3. `ssh-keygen`# 会出现下面的内容，一直按Enter键就行；
4. 打开用户目录下的 `.ssh`目录下面生成 `id_rsa(私钥)id_rsa.pub(公钥)`两个文件，打开`id_rsa.pub`，复制里面的内容,到 github: `Settings -> New SSH key -> SSH and GPG keys -> (填写)Title -> (粘贴)Key -> Add SSH Key`；
5. 测试 `ssh -T git@github.com`，**输出 You’ve successfully authenticated 表示添加key 成功。**

### 六、安装 hexo

```
npm install hexo-cli -g
```

### 七、将原博客备份文件复制至username.github.io文件夹

**_config.yml，theme/，source/，scaffolds/，package.json，.gitignore，6 个文件需要拷贝。**

**需要备份的文件如下:**

1. 站点配置`_config.yml`；
2. `theme`文件夹里面的主题；
3. `source`文件夹；
4. `scaffolds`文件夹（文章的模板）；
5. `package.json`（说明使用哪些包）；
6. `.gitignore`（限定在提交的时候哪些文件可以忽略）；

总结：**_config.yml，theme/，source/，scaffolds/，package.json，.gitignore，6 个文件需要拷贝。**

**注意：****不要hexo init去整体初始化**

### 九、提交本地至XXX分支

进入username.github.io文件目录下，依次执行：
1. `git add`.

2. `git commit -m ‘新电脑部署’`（引号内容可改）

3. `git push`

这样，`master分支`用于保存博客静态资源，提供博客页面供人访问；`xxx分支`用于备份博客部署文件，供自己修改和更新，两者在一个GitHub仓库内互不冲突。

### 十、安装 hexo 依赖的包

```
npm install
```

所依赖的包都在上一步中的`package.json`备份文件里，所以直接这一个命令就可以了。

### 十一、新旧电脑更新博客

1. `git pull`；
2. `hexo n xxx`，编辑、撰写文章或其他博客更新改动，就是你要对博客进行的修改，或新增文章；
3. `hexo clean` // 可选；
4. `hexo g`；
5. `hexo s`；
6. `hexo d`。
7. `git add .`；
8. `git commit -m ‘在新电脑上提交新文章’`（引号内容可改）;
9. `git push`指令，保证xxx分支版本为最新版本。

从上述第 4 步后可以这样子发布：

```
hexo g -d && git add . && git commit -m  "更新" && git push && exit
```

OK !