---
title: GitHub Pages 玩不转
date: 2017-12-02 11:32:37
tags:
---

> # 玩不转的`GitHub Pages`

 玩转玩不转, 就是把免费的博客搞起来. 非高端教程 ^_^

## 准备工作
 你所需要的环境

### GitHub

* 首先的申请一个账号`GitHub` [传送门](https://github.com/)
* 登录后, 创建一个新的仓库,并且以 `username.github.io` 为仓库名, 这儿的username是你自己的`GihtHub` 账号名 

### Node

* Windows 下直接去官网 [下载](https://nodejs.org/en/)

* 安装完成后使用命令 `node -v` 检测是否安装成功

### Hexo

 Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
* 在node 装好后, 使用命令 `npm install hexo-cli -g` 安装 hexo脚手架工具
* 更多指导跳[官网](https://hexo.io/)

### 看到你的 `Hello World`

* 首先把 `username.github.io` 这个版本 `clone` 到本地
* 然后在 `cd username.github.io` 进入该版本库
* 创建一个名为 `hexo` 的分支 `git checkout -b hexo`
* 创建 `Hexo` 项目  `hexo init`
* 安装依赖 `npm i`
* 修改配置信息 `_config.yml`
    * 修改网站的 `title` 之类 , 详细参考[Hexo 玩不转](/blog/4fce4897)
    * 主要是填写 版本库的地址

    ```
     deploy:
        type: git
        repo: https://github.com/MasterShu/mastershu.github.io.git  - 这儿填写你自己的地址
        branch: master
    ```

* 上传 `GitHub`
    * 安装依赖 `npm install hexo-deployer-git --save`
    * 执行上传, 上传过程中可能需要输入你自己的 `GitHub` 账号密码
        ```
        hexo clean
        hexo generate
        hexo deploy
        ```
    * 然后访问 `http://username.github.io` 就可以看到自己的博客了

### 免费的博客

    进行的这一步, 其实已经完成了自己的 `GitHub Pages` 的主要操作了, 对于SEO之类的, 反正我不是很懂, 就是为了 装*, 接下来, 就是配置自己的域名访问
* 首先的注册一个域名, 阿里云, 腾讯云之类的都可以, 不打广告
* 就行域名解析, 
    * 获取要解析的域名IP `ping username.github.io` 获取你的自己的IP 
    * 解析一个二级域名到该IP `blog`
* 配置 `GItHub` 上的自定义 `Custom domain` ,输入自己刚才解析的 `blog.userdomain.name` , 在版本的 `setting` 下
* 至此, 一个免费的博客就完成了, 可以通过你自己的域名访问的博客