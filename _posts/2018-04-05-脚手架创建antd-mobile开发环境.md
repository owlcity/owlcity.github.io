---
title: webpack antd-mobile
date: 2018-04-05 17:30:09
categories:
- Javascript
tags:
- webpack 
- antd
---

### (转：https://blog.csdn.net/Wu_shuxuan/article/details/78832384)Facebook 官方推出Create-React-App脚手架，基本可以零配置搭建基于webpack的React开发环境，内置了热更新等功能。

**使用的原因以及特性:**

 * 无需配置；
 * 集成了对 React, JSX, ES6 和 Flow 的支持；
 * 集成了开发服务器；
 * 配置好了浏览器热加载的功能；
 * 在 JavaScript 中可以直接 import CSS 和图片；
 * 自动处理 CSS 的兼容问题，无需添加 -webkit 前缀；
 * 集成好了编译命令，编译后直接发布成产品，并且还包含了 sourcemaps。

**创建项目:**

``` javascript
 npm install -g create-react-app       /* 安装create-react-app，建议使用cnpm */
 create-react-app register                 /* 使用命令创建应用，myapp为项目名称 */
 cd register                                 /* 进入目录，然后启动 */
 npm start
```
**生成的项目目录：**

![img01](/assets/images/article/antd_1.png)

### 在webstorm中输入 npm start 在浏览器中即可看到欢迎页面

![img01](/assets/images/article/antd_2.png)

### antd-mobile的引入及配置

执行命令行：:

``` javascript
npm install antd-mobile --save
```

### 按需引入

``` javascript
yarn add react-app-rewired --dev
```

``` javascript
/* package.json */
"scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
-   "test": "react-scripts test --env=jsdom",
+   "test": "react-app-rewired test --env=jsdom",
}
```

然后在项目根目录创建一个 config-overrides.js 用于修改默认配置。

``` javascript
module.exports = function override(config, env) {
  // do stuff with the webpack config...
  return config;
};
```

使用 babel-plugin-import, babel-plugin-import 是一个用于按需加载组件代码和样式的 babel 插件（原理），现在我们尝试安装它并修改 config-overrides.js 文件。

``` javascript
yarn add babel-plugin-import --dev
```

``` javascript
+ const { injectBabelPlugin } = require('react-app-rewired');
  module.exports = function override(config, env) {
+   config = injectBabelPlugin(['import', { libraryName: 'antd-mobile', style: 'css' }], config);
    return config;
  };
```

更改引用方式

``` javascript
- import Button from 'antd-mobile/lib/button';
+ import { Button } from 'antd-mobile';
```

使用表单时，受控组件要安装 rc-form


``` javascript
npm install rc-form --save-dev
```

运行时输入：

``` javascript
yarn start
```

![img01](/assets/images/article/antd_3.png)

示例代码在github上 ：
[git代码](https://github.com/owlcity/ant-design-mobile-1)

##### 1. 下载项目到本地

##### 2. 安装依赖

``` javascript
npm install
```

##### 3.输入 yarn start , http://localhost:3000/ 显示成功。

![img01](/assets/images/article/antd_3.png)


##### 4. 项目配置

生成项目后，脚手架为了“优雅”隐藏了所有的webpack相关的配置文件，此时查看myapp文件夹目录，会发现找不到任何webpack配置文件。执行以下命令：

``` javascript
npm run eject
```

![img01](/assets/images/article/antd_5.png)

运行时是直接执行scripts文件目录下的js文件

![img01](/assets/images/article/antd_6.png)

### 使用 React Router说明

##### 注意

``` javascript
1. Node 的版本必须 >= 4，推荐 Node >= 6 and npm >= 3；
2. 运行起来后浏览器已经实现了热加载刷新，修改代码保存后浏览器会自动刷新；
3. 执行 npm test 或 yarn test 可以执行测试动作，更多请参阅这里；
4. 编译项目执行 npm run build 或 yarn build；
```