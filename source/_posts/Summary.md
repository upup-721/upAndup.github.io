---
title: 问题总结及注意事项
date: 2024-01-06 09:58:29
description: 搭建及使用hexo常见问题记录，以便后续更换设备或遇到bug作为参考
tags: 
  - practice
  - problems
  - attention
categories:
  - 测试练习
cover: cover.png
keywords: "hexo,搭建,hexo-renderer-marked,git,问题"
---

{% note green 'fas fa-bullhorn' flat %}

本篇为入门，旨在记录初次搭建使用`hexo`的一些踩坑经历

{% endnote %}

<span id="jump2"></span>

## &#x1F517;  [本地搭建hexo步骤](#jump2)

{% note blue flat %}

利用`github`的分支快速搭建与备份

1. hexo分支作为默认分支，存放基本的配置信息，更新文章或更改配置需要push到该分支
2. main分支用来部署hexo文章，交由 GitHub Pages 托管

详见这篇[Hexo在多台电脑上提交和更新_hexo 多机更新-CSDN博客](https://blog.csdn.net/K1052176873/article/details/122879462)(...感谢大佬)

{% endnote %}

### clone仓库到本地（clone的是默认分支，即我的hexo分支）

``` bash
git clone git@github.com:username/username.github.io.git
---
git clone git@github.com:upup-721/upup-721.github.io.git
```

### 下载依赖

```bash
npm install hexo
npm install
npm install hexo-deployer-git
```

>1. 可用`npm list`检查依赖列表及版本，我当前使用如下
>
>```bash
>hexo-site@0.0.0 D:\MyBlog\hexo_butterfly\upup-721.github.io
>+-- hexo-deployer-git@4.0.0
>+-- hexo-generator-archive@2.0.0
>+-- hexo-generator-category@2.0.0
>+-- hexo-generator-index@3.0.0
>+-- hexo-generator-search@2.4.3
>+-- hexo-generator-tag@2.0.0
>+-- hexo-lazyload-image@1.0.13
>+-- hexo-renderer-ejs@2.0.0
>+-- hexo-renderer-marked@6.2.0
>+-- hexo-renderer-pug@3.0.0
>+-- hexo-renderer-stylus@2.1.0
>+-- hexo-server@3.0.0
>+-- hexo-theme-butterfly@4.12.0
>+-- hexo-theme-landscape@0.0.3
>`-- hexo@6.3.0
>```
>
>2. 检查butterfly主题是否下载成功，获取备份复制到theme文件夹下

### 依次执行`hexo clean、hexo g、hexo s`，看能否正常在本地预览

### 一切正常即可`hexo new ""`开始愉快写作啦，注意每更新文章或配置要提交到远程仓库

```bash
git add .
git commit –m add_branch
git push
```

-----

<span id="jump1"></span>

## &#x1F517;  [解决hexo文章中插入图片的问题](#jump1)

{% note flat %}

困扰了我两晚上，害我重新搭了三四次环境，最后发现居然是因为npm的源有问题以及装了一个已经废弃的包。。。万恶的`hexo-asset-image@1.0.0`  (&#x1F62D;一些菜鸡自述)

{% endnote %}

>__文章最终要部署在网站上，部署后会生成新的文件目录，因此图片应采取相对目录__
>
>解决方法其实并不难:
>
>1. npm安装插件[hexo-renderer-marked](https://link.zhihu.com/?target=https%3A//github.com/hexojs/hexo-renderer-marked)，并在hexo根目录的config.yml中更改配置：
>
>```yaml
>post_asset_folder: true  # hexo new创建文章时生成同名文件夹
>marked:
>  prependRoot: true
>  postAsset: true
>```
>
>2. hexo文章中只需直接使用`![](image.jpg)`愉快的插入图片

{% note orange flat %}

__参考链接__:

[hexo文章插入图片方法小结_hexo 图片-CSDN博客](https://blog.csdn.net/u014155600/article/details/128950724)

[hexo博客如何插入图片 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/265077468)

[Hexo 常用插件推荐-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/2143602)

[一文详解NPM如何换源_node.js_脚本之家 (jb51.net)](https://www.jb51.net/article/273979.htm)

{% endnote %}

