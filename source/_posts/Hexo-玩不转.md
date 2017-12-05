---
title: Hexo 玩不转
abbrlink: 4fce4897
date: 2017-12-02 14:14:06
tags: 
  - 玩不转
category: "UnableToManage"
---
## 玩转玩不转的`Hexo`

官方指导, 是最具有权威的指导, 但是我依然要写这篇文章, 是为了让你能快速开发, 并且给出一些个人建议, 更多细节请参考[官网](https://hexo.io/)

本文即是在 `Next` 主题下实现, 而其中的某些配置也是配合该主题使用的, 本人也会在配置上说明

## 准备工作

    这儿是配置必要的环境, 已经配置好的请跳过

<!-- more -->

### Node

* Windows 下直接去官网 [下载](https://nodejs.org/en/)

* 安装完成后使用命令 `node -v` 检测是否安装成功

### Hexo

 Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
* 在node 装好后, 使用命令 `npm install hexo-cli -g` 安装 hexo脚手架工具
* 更多指导跳[官网](https://hexo.io/)

## 文章链接永久化

* 安装依赖

    ```base
    npm i hexo-abbrlink -S
    ```

* 配置`Permalink`

    ```YML
    permalink: blog/:abbrlink/  - 此处的blog可换成任意你喜欢的目录
    ```
* 添加配置

    ```YML
    # abbrlink config
    abbrlink:
    alg: crc32  # 算法：crc16(default) and crc32
    rep: hex    # 进制：dec(default) and hex
    可选择的算法:
    crc16 & hex
    crc16 & dec
    crc32 & hex
    crc32 & dec
    ```

## Next 主题

本人仅选择一个主题作为介绍, 其他主题的用法或者功能或有不同, 不过可以参考和类推 [自制主题](https://hexo.io/zh-cn/docs/themes.html) [Next 主题](http://theme-next.iissnan.com/)

### Quick Start

```base
 cd your-hexo-site
 git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### next主题集成gitment评论系统

当然`Next`主题中也包含了很多主题, 习惯了github的邮箱推送, 可能其他评论系统也有,  请自行[发掘]()
这个评论主要是把评论放到github的issues系统里.

#### 注册Oauth

[点击注册](https://github.com/settings/applications/new)  `Authorization callback URL` 就是你要申请登录的网站

#### 修改配置

* `next` 主题配置 `_config.yml` 添加

```YML
# Gitment
# Introduction: https://imsun.net/posts/gitment-introduction/
gitment:
    enable: true
    githubID: yourid
    repo: yourrepo
    ClientID: yourid
    ClientSecret: yoursecret
    lazy: true
```

* 主题`next`目录下 `languages/en.yml` 添加

```YML
gitmentbutton: Show comments from Gitment
```

* 主题`next`目录下 `languages/zh-Hans.yml`增加:

```YML
gitmentbutton: 显示 Gitment 评论
```

#### 添加gitment评论判断

在`layout/_partials/comments.swig` 

```bash
    {% elseif theme.changyan.appid and theme.changyan.appkey %}
      <div id="SOHUCS"></div>
```

下新增

```bash
    {% elseif theme.gitment.enable %}
       {% if theme.gitment.lazy %}
         <div onclick="ShowGitment()" id="gitment-display-button">{{  __('gitmentbutton') }}</div>
         <div id="gitment-container" style="display:none"></div>
       {% else %}
         <div id="gitment-container"></div>
       {% endif %}
```

#### 添加`gitment`显示文件

在`layout/_third-party/comments/`目录下中添加文件`gitment.swig`
并且引入在`layout/_third-party/comments/index.swig`文件中引入 `include 'gitment.swig'`

```swig
{% if theme.gitment.enable %}
   {% set owner = theme.gitment.githubID %}
   {% set repo = theme.gitment.repo %}
   {% set cid = theme.gitment.ClientID %}
   {% set cs = theme.gitment.ClientSecret %}
   <link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
   <script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
   {% if not theme.gitment.lazy %}
       <script type="text/javascript">
           var gitment = new Gitment({
               id: window.location.pathname, 
               owner: '{{owner}}',
               repo: '{{repo}}',
               oauth: {
                   client_id: '{{cid}}',
                   client_secret: '{{cs}}',
               }});
           gitment.render('gitment-container');
       </script>
   {% else %}
       <script type="text/javascript">
           function ShowGitment(){
               document.getElementById("gitment-display-button").style.display = "none";
               document.getElementById("gitment-container").style.display = "block";
               var gitment = new Gitment({
                   id: document.location.href, 
                   owner: '{{owner}}',
                   repo: '{{repo}}',
                   oauth: {
                       client_id: '{{cid}}',
                       client_secret: '{{cs}}',
                   }});
               gitment.render('gitment-container');
           }
       </script>
   {% endif %}
{% endif %}
```

#### 添加`gitment`样式

在主题目录下 `source/css/_common/components/third-party/` 下添加`gitment.styl`文件
并且在 `source/css/_common/components/third-party/third-party.styl` 下引入 `@import "gitment";`

```css
#gitment-display-button{
     display: inline-block;
     padding: 0 15px;
     color: #0a9caf;
     cursor: pointer;
     font-size: 14px;
     border: 1px solid #0a9caf;
     border-radius: 4px;
 }
 #gitment-display-button:hover{
     color: #fff;
     background: #0a9caf;
 }
 ```

## 迁移

> 迁移操作很简单, 更多详见 [官方指南](https://hexo.io/zh-cn/docs/migration.html)

* 目标: Jekyll
* 操作: 把 _posts 文件夹内的所有文件复制到 source/_posts 文件夹，并在 _config.yml 中修改 new_post_name 参数。
  `new_post_name: :year-:month-:day-:title.md`

## 标签与分类

### 创建页面

> 标签与分类, 是为了更好的规整文档, 本段是配合`next`主题使用的

  ```base
  cd your-hexo-site 
  hexo new page tags  # 创建标签页面
  hexo new page categories  # 创建分类页面
  ```

### 修改页面类型

分别在刚才添加的分类和标签页面 添加`type` 以及 `comments` 评论功能关闭
  ```md
  ---
  title: categories
  date: 2017-12-05 11:38:23
  type: "categories"
  comments: false
  ---

  ---
  title: categories
  date: 2017-12-05 11:38:23
  type: "tags"
  comments: false
  ---
  ```

### 修改配置文件

修改菜单显示 在主题的配置文件 `_config.yml` 中添加标签和分类
  ```yml
  menu:
    home: /
    archives: /archives/
    tags: /tags/
    categories: /categories/
  ```

### 使用标签和分类

在新建的文章中,添加`tags` 以及 `categories`即可. 示例:
  ```markdown
  ---
  title: Hexo 玩不转
  abbrlink: 4fce4897
  date: 2017-12-02 14:14:06
  tags: 
    - 玩不转
  category: 
    - 实践先锋
  ---
  ```

## Tag Plugins 标签插件

> 标签插件是用于在文章中快速插入特定内容的插件。

### Quote 引用块

> 这儿只做简单示例, 更多使用请查看[官网](https://hexo.io/zh-cn/docs/tag-plugins.html)

  ```base
  {% blockquote [author[, source]] [link] [source_link_title] %}
  content
  {% endblockquote %}
  ```

例如:
  ```base
  {% blockquote Hexo https://hexo.io/news/ Hexo 3.2 Released %}
  It has been a long time that Hexo is poor at handling large website. (#710, #1124, #283, #1187, #550, #1769, etc.) We tried hard to solve this problem and there’re several improvements in Hexo 3.2.
  {% endblockquote %}
  ```
显示效果
  {% blockquote Hexo https://hexo.io/news/ Hexo 3.2 Released %}
  It has been a long time that Hexo is poor at handling large website. (#710, #1124, #283, #1187, #550, #1769, etc.) We tried hard to solve this problem and there’re several improvements in Hexo 3.2.
  {% endblockquote %}

## 资源与数据

> 这段主要讨论的是如何合理的使用资源和数据, 我会列出 `Hexo` 官方的做法, 以及个人的想法

### 资源文件夹

#### 基本加载方式

最简单的方法就是将它们放在 `source/images` 文件夹中。然后通过类似于 `![](/images/image.jpg)` 的方法访问它们。

#### 相对路径引用的标签插件

1. 修改配置文件`_config.yml`
  `post_asset_folder: true`
2. 相对路径引用标签
  `{% asset_img example.jpg This is an example image %}`

  ```base
  正确的引用图片方式是使用标签插件而不是 markdown
  ```
以上是官网给的回答, 个人认为`Markdown`的比较简单好用, 而且学习一个新的标签语法用来写博客也会增加学习成本. (毕竟就只是写个博客而已^_^)

### 数据文件夹

> Hexo 3.0 新增的「数据文件」功能。此功能会载入 source/_data 内的 YAML 或 JSON 文件.

举例来说，在 source/_data 文件夹中新建 menu.yml 文件：
  ```yml
  Home: /
  Tags: /tags/
  Archives: /archives/
  ```
您就能在模板中使用这些资料：
  ```base
  <% for (var link in site.data.menu) { %>
    <a href="<%= site.data.menu[link] %>"> <%= link %> </a>
  <% } %>
  ```
渲染结果如下 :
  ```base
  <a href="/"> Home </a>
  <a href="/tags/"> Tags </a>
  <a href="/archives/"> Archives </a>
  ```
