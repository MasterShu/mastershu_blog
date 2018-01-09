---
title: 初探 React
abbrlink: 94177a20
tags:
---

# React 的初探

React 一个由 `FaceBook` 出品的 `JavaScript` 框架. 作为目前前端框架三巨头之一, 由于前段时间的开源协议问题, 现在已经更新了协议, 那就让我们来了解一下 `React`

## Quick Start

### 准备工作

* `Node` 环境

* 安装脚手架工具 `npm i -g create-react-app`

另一个选择, `node` 的最新长期 `LTS` 版本已经到 `8.9.1` 了, `React` 就给了我们另外一个选择 `npx`

* `npx create-react-app <project>` 指令来初始化项目

但是 `npx` 要钱 `npm 5.2.0+` 所以我的示例依然使用第一种来创建. 这个的采用由个人喜好

### Hello React

首先新建项目
  ```base
  create-react-app <project>
  ```

然后进入项目目录,启动初始化的项目
  ```base
  npm start
  ```

现在, 你已经看到新建立的网站了, 地址是 `http://localhost:3000/`

接下来就是重头戏了, 打开项目目录, 在源码目录 `src` 下面找到 `App.js` 这个就是首页展示的内容

更改你的需要, 把 `Welcome to React` 改为 `Hello React`, 再次回到浏览器页面.

`Hello React` 你已经很棒了.

# ToDoList

按照惯例, 第一个实现的简单的功能就是 `ToDoList` 了

## 安装 UI 组件库

这里推荐一款比较喜欢的组件库 `Element` , 可能你会说这个不是 `Vue` 的吗, 嘿嘿 [传送门](https://eleme.github.io/element-react/)

### 引入 UI 库

安装
  ```base
  npm i element-react -S
  ```
这个还需主题包
  ```base
  npm i element-theme-default -S
  ```
