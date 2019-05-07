# AngElectron2

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 7.3.8.

## 运行

1、安装 package，在项目录下运行 `npm install` 命令,因为墙的原因可能无法下载一些库，可以使用 [cnpm](https://npm.taobao.org) 或 [yarn](https://yarnpkg.com/zh-Hans/)。

2、使用 `ng serve` 调试项目，项目访问地址为 [http://localhost:4200/](http://localhost:4200/) 。文件改变时app自动刷新

## electron 安装打包更新配置

需求： 将已完成好的Angular项目封装成一个桌面应用；Electron 可以让你使用纯 JavaScript 调用丰富的原生 APIs 来创造桌面应用

## 创建项目

ng new ang-electron2

## 打包步骤

1、在ang-electron2项目package.json目录下执行npm install electron --save

2、创建main.js文件 ![Image text](https://github.com/yujiao-qunar/Angular-electron/blob/master/src/assets/img/lib.png)

3、main.js内容
```

const {app, BrowserWindow} = require('electron')
const path = require('path')
const url = require('url')

// 保持一个对于 window 对象的全局引用，如果你不这样做，
// 当 JavaScript 对象被垃圾回收， window 会被自动地关闭
let win

function createWindow () {
  // 创建浏览器窗口。
  win = new BrowserWindow({width: 800, height: 600})

  // 然后加载应用的 index.html。
  win.loadURL(url.format({
    pathname: path.join(__dirname, 'dist/ang-electron2/index.html'),
    protocol: 'file:',
    slashes: true
  }))

  // 打开开发者工具。
  // win.webContents.openDevTools()

  // 当 window 被关闭，这个事件会被触发。
  win.on('closed', () => {
    // 取消引用 window 对象，如果你的应用支持多窗口的话，
    // 通常会把多个 window 对象存放在一个数组里面，
    // 与此同时，你应该删除相应的元素。
    win = null
  })
}

// Electron 会在初始化后并准备
// 创建浏览器窗口时，调用这个函数。
// 部分 API 在 ready 事件触发后才能使用。
app.on('ready', createWindow)

// 当全部窗口关闭时退出。
app.on('window-all-closed', () => {
  // 在 macOS 上，除非用户用 Cmd + Q 确定地退出，
  // 否则绝大部分应用及其菜单栏会保持激活。
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // 在macOS上，当单击dock图标并且没有其他窗口打开时，
  // 通常在应用程序中重新创建一个窗口。
  if (win === null) {
    createWindow()
  }
})

// 在这文件，你可以续写应用剩下主进程代码。
// 也可以拆分成几个文件，然后用 require 导入。

```

4、修改package.json文件增加electron的相关配置
![Image text](https://github.com/yujiao-qunar/Angular-electron/blob/master/src/assets/img/package.png)

5、运行项目 npm run start
![Image text](https://github.com/yujiao-qunar/Angular-electron/blob/master/src/assets/img/elec.png)

## tips

1、此项目可直接下载使用

2、开启调试模式,在main.js注释掉win.webContents.openDevTools()再次编译即可。

3、运行后项目路径有问题的，index.html文件中的``` <base href="/"> ```替换成``` <base href="./">```

4、项目http请求使用代理的，将environment的baseUrl替换为实际访问地址

5、项目css的png无法显示，改为行内可显示

## 打包

1、安装打包工具：npm install electron-packager --save

2、如上图，添加打包脚本

3、打包： npm run package

4、exe文件安装
![Image text](https://github.com/yujiao-qunar/Angular-electron/blob/master/src/assets/img/final.png)

## 更新

待续。。。



