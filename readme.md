# glorious-codes/glorious-demo [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 演示代码的最简单方法.(web) 」

[中文](./readme.md) | [english](https://github.com/glorious-codes/glorious-demo)

---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'glorious-codes/glorious-demo' -->
<!-- commit = '5d43a5166803eba6fc5525979f6441569793332b' -->
<!-- time = '2018-11-09' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-11-09 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/glorious-codes/glorious-demo.svg
[commit]: https://github.com/glorious-codes/glorious-demo/tree/5d43a5166803eba6fc5525979f6441569793332b

<!-- doc-templite END generated -->

- [x] [存储库维基百科](https://github.com/chinanf-boy/glorious-demo-zh/wiki)

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

# glorious 的演示

> 演示代码的最简单方法.

[![CircleCI](https://circleci.com/gh/glorious-codes/glorious-demo.svg?style=svg)](https://circleci.com/gh/glorious-codes/glorious-demo)
[![codecov](https://codecov.io/gh/glorious-codes/glorious-demo/branch/master/graph/badge.svg)](https://codecov.io/gh/glorious-codes/glorious-demo)

<p align="center">
  <img src="https://user-images.githubusercontent.com/4738687/44633197-01fa4900-a95e-11e8-9b53-66e9043e2533.gif" />
</p>

### 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [安装](#%E5%AE%89%E8%A3%85)
- [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)
  - [API](#api)
    - [`openApp`](#openapp)
    - [`write`](#write)
    - [`command`](#command)
    - [`respond`](#respond)
    - [`end`](#end)
- [贡献](#%E8%B4%A1%E7%8C%AE)
- [测试](#%E6%B5%8B%E8%AF%95)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 安装

```
npm install @glorious/demo --save
```

## 基本用法

```html
<link rel="stylesheet" href="node_modules/@glorious/demo/dist/gdemo.min.css" />
<script src="node_modules/@glorious/demo/dist/gdemo.min.js"></script>
```

_注意:如果您不使用包管理器,请从第三方[CDN 提供商](https://github.com/chinanf-boy/glorious-demo-zh/wiki/CDN-Providers-zh)加载._

```javascript
// 构造函数,接收 selector 的 指示
// 也就是在您的页面中，注入演示的位置。
const demo = new GDemo('#container');

const code = `
function greet(){
  console.log("Hello World!");
}

greet();
`;

demo
  .openApp('editor', {minHeight: '350px', windowTitle: 'demo.js'})
  .write(code, {onCompleteDelay: 1500})
  .openApp('terminal', {minHeight: '350px', promptString: '$'})
  .command('node ./demo', {onCompleteDelay: 500})
  .respond('Hello World!')
  .command('')
  .end();
```

_注意:查看[这里](https://github.com/chinanf-boy/glorious-demo-zh/wiki/Syntax-highlight-zh)知道如何使用 Prism 来高亮您的代码._

### API

#### `openApp`

打开或最大化打开的应用程序.

```javascript
/*
 ** @applicationType: String [required]
 ** @options: Object [optional]
 */

// 可能的值是'editor'或'terminal'
const applicationType = 'terminal';

const openAppOptions = {
  minHeight: '350px',
  windowTitle: 'bash',
  promptString: '~/my-project $', // 仅适用于“terminal”应用程序
  onCompleteDelay: 1000 // 执行下一个方法之前的延迟
};

demo.openApp(applicationType, openAppOptions).end();
```

#### `write`

在打开的编辑器应用程序中，写入一些代码.

```javascript
/*
 ** @codeSample: String [required]
 ** @options: Object [optional]
 */

// 标签和换行符将被保留
const codeSample = `
function sum(a, b) {
  return a + b;
}

sum();
`;

const writeOptions = {
  onCompleteDelay: 500 // 执行下一个方法之前的延迟
};

demo
  .openApp('editor')
  .write(codeSample, writeOptions)
  .end();
```

#### `command`

在打开的终端应用程序中，写入一些命令.

```javascript
/*
 ** @command: String [required]
 ** @options: Object [optional]
 */

const command = 'npm install @glorious/demo --save';

// 为此命令和以下命令重新定义提示字符串
const promptString = '$';

// 可以选择是HTML字符串：
const promptString = '<span class="my-custom-class">$</span>';

const commandOptions = {
  promptString,
  onCompleteDelay: 500 // 执行下一个方法之前的延迟
};

demo
  .openApp('terminal')
  .command(command, commandOptions)
  .end();
```

#### `respond`

在打开的终端应用程序上，显示一些响应.

```javascript
/*
 ** @response: String [required]
 ** @options: Object [optional]
 */

// 换行符将被保留
const response = `
+ @glorious/demo successfully installed!
+ v0.1.0
`;

// 可以选择, HTML字符串：
const response = `
<div><span class="my-custom-class">+</span> @glorious/demo successfully installed!</div>
<div><span class="my-custom-class">+</span> v0.6.0</div>
`;

const respondOptions = {
  onCompleteDelay: 500 // 执行下一个方法之前的延迟
};

demo
  .openApp('terminal')
  .respond(response, respondOptions)
  .end();
```

#### `end`

表示演示结束。不要忘记在演示结束时，调用它。否则,将不会播放演示.

## 贡献

1.  安装[node](https://nodejs.org/en/)。下载"推荐给大多数用户"版本.

2.  克隆回购:

```bash
git clone git@github.com:glorious-codes/glorious-demo.git
```

3.  转到项目目录:

```bash
cd glorious-demo
```

4.  安装项目依赖项:

```bash
npm install
```

5.  建立项目:

```bash
npm run build
```

## 测试

确保您添加的所有代码，都包含在单元测试中:

```bash
npm run test -- --coverage
```
