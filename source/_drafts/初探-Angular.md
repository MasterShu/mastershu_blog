---
title: 初探 Angular
tags:
  - Angular
  - JavaScript
  - Node
category:
  - 框架学习
  - 前端框架
  - Angular
abbrlink: '72960925'
---

# Angular 的初探

一直收到论坛和其他文章的影响, 觉得 `Angular` 学习曲线很陡, 不适合新手入门, 而且很重, 性能不好.

这些都是道听途说, 不一定是什么样的, 所以本人想亲自试一下! 参考教程中文官网 [传送门](https://angular.cn)

## Quick Start

来看看官方是如何介绍的
{% blockquote angular.cn https://angular.io/docs  What is Angular? %}
  Angular is a platform that makes it easy to build applications with the web. Angular combines declarative templates, dependency injection, end to end tooling, and integrated best practices to solve development challenges. Angular empowers developers to build applications that live on the web, mobile, or the desktop
{% endblockquote %}

<!--more-->

### 准备工作

* `Node` 环境

* 安装脚手架工具 `npm install -g @angular/cli`

### Hello Angular

国内的镜像还是蛮有用的, 让我们设置一下吧
  ```base
  ng set --global packageManager=cnpm
  ```
新建项目
  ```base
  ng new <project>
  ```
土包子长见识了, `new` 之后会自动执行, `npm install` 所以, 各位最好是先执行全局设置 `cnpm`

运行服务器
  ```base
  ng serve --open
  ```

好了, 已经可以看到我们的网站了, 那么让我们写下第一行代码. 在项目的 `src` 目录下面, `app` 这个代码目录下, `Angular` 会自动创建一个 `app-root` 的组件, 在`app.component.ts`修改为:
  ```ts
  export class AppComponent {
    title = 'Angular';
  }
  ```

再次回到网页, 就会看到 `Welcome to Angular!` 你已经能用 angular 了

# ToDoList

让我们使用 `Angular` 实现我们的第一个功能吧

## 安装 UI 组件库

这里推荐一款比较喜欢的组件库 `Element` , 可能你会说这个不是 `Vue` 的吗, 嘿嘿 [传送门](https://element-angular.faas.ele.me)

```base
# npm i -S element-angular
```

### 引入 UI 库

```ts
// in /src/app/app.module.ts
// add code:

// improt element module
import { ElModule } from 'element-angular'

// 并且在 imports 中添加引入
  imports: [
    BrowserModule,
    ElModule.forRoot(), // 新增引入
  ],
```

```css
// in /src/styles.css
// add code:

/* You can add global styles to this file, and also import other style files */
@import "~element-angular/theme/index.css";
```

## 路由

## 
