---
title: Hexo 玩不转
date: 2017-12-02 14:14:06
tags:
---
# 玩转玩不转的`Hexo`
官方指导, 是最具有权威的指导, 但是我依然要写这篇文章, 是为了让你能快速开发, 并且给出一些个人建议, 更多细节请参考[官网](https://hexo.io/)
## 准备工作

    这儿是配置必要的环境, 已经配置好的请跳过

### Node

* Windows 下直接去官网 [下载](https://nodejs.org/en/)

* 安装完成后使用命令 `node -v` 检测是否安装成功

### Hexo

 Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
* 在node 装好后, 使用命令 `npm install hexo-cli -g` 安装 hexo脚手架工具
* 更多指导跳[官网](https://hexo.io/)


## 文章链接永久化

* 安装依赖
    ```
    npm i hexo-abbrlink -S
    ```
* 配置`Permalink`
    ```
    permalink: blog/:abbrlink/  - 此处的blog可换成任意你喜欢的目录
    ```
* 添加配置
    ```    
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
### Quick Start
### next主题集成gitment评论系统
这个评论主要是把评论放到github的issues系统里.
#### 注册Oauth
[点击注册](https://github.com/settings/applications/new) 
* `Authorization callback URL` 就是你要申请登录的网站
#### 修改配置
* `next` 主题配置 `_config.yml` 添加
```
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
```
gitmentbutton: Show comments from Gitment
```

* 主题`next`目录下 `languages/zh-Hans.yml`增加:
```
gitmentbutton: 显示 Gitment 评论
```

### 修改主题
#### 添加gitment评论判断
在`layout/_partials/comments.swig` 
```
    {% elseif theme.changyan.appid and theme.changyan.appkey %}
      <div id="SOHUCS"></div>
```
下新增
```
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
并且引入在`layout/_third-party/comments/index.swig`文件中引入 `{% include 'gitment.swig' %}`

```
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
```
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