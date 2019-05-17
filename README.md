基于 Lodop 的 web 打印示例
---

1. [概述](#1-概述)
2. [相关资源](#2-相关资源)
3. [一个发运单打印的 Demo](#3-一个发运单打印的-demo)
4. [关于连打](#4-关于连打)
	- 4.1. [连打关键点](##41-连打关键点)
	- 4.2. [具体实现方法](#42-具体实现方法)
5. [附录](#5-附录)
	- 5.1. [相关常见问题](#51-相关常见问题)
	- 5.2. [纸型说明](#52-纸型说明)

---

### 1. 概述

Lodop & C-Lodop 是一款专业共享软件，公开版本未限制功能，多数用户可免费长期使用。

仅如下情况需要**注册收费**：

- 你希望用到（不经过弹出预览窗口的）「直接打印」功能时，如果不注册，该功能直接打印的纸张左下角会有“*本页由XXX试用版输出*”小字样水印。
- 另外，导出Excel文件或图片也需要注册。

### 2. 相关资源

- 官网下载中心（程序+文档）：[http://www.lodop.net/download.html](http://www.lodop.net/download.html)
- 官方打印示例：[http://www.lodop.net/demo.html](http://www.lodop.net/demo.html)
- 常见问题列表：[http://www.lodop.net/problem.html](http://www.lodop.net/problem.html)

### 3. 一个发运单打印的 Demo

示例的目录结构说明

```text
.
├── assets
│   ├── images
│   │   ├── layer-btn-cancel-hover.png
│   │   ├── layer-btn-cancel.png
│   │   ├── layer-btn-ok-hover.png
│   │   ├── layer-btn-ok.png
│   │   ├── layui-layer-title-close-hover.png
│   │   ├── layui-layer-title-close.png
│   │   └── layui-layer-title-info.png
│   ├── jquery.min.js
│   ├── jquery.tmpl.js     <----- 一个简单的模块数据渲染插件
│   ├── layer     <----- 本示例使用 layer 处理消息弹窗
│   │   ├── extend
│   │   │   └── layer.ext.js
│   │   ├── layer.js
│   │   └── skin
│   │       ├── default
│   │       │   ├── icon-ext.png
│   │       │   ├── icon.png
│   │       │   ├── loading-0.gif
│   │       │   ├── loading-1.gif
│   │       │   └── loading-2.gif
│   │       ├── layer.css
│   │       └── layer.ext.css
│   ├── lodop     <----- 打印插件相关文件
│   │   ├── CLodop_Setup_for_Win32NT.exe
│   │   ├── LodopFuncs.js
│   │   ├── install_lodop32.exe
│   │   └── install_lodop64.exe
│   └── my.js     <----- 一些用到的公共函数：转换金额、时间，调用弹窗
├── data.json     <----- 模拟数据
└── index.html     <----- 示例页：打印控件的调用及打印样式设置等
```

点击打印后，打印预览效果如下

![预览图片）](./screenhot.png)


### 4. 关于连打

#### 4.1. 连打关键点

> 连打时主要是通过「针式打印机」，使用三联n等分的打印纸进行批量打印。关于纸型的说明，详见附录：[5.2. 纸型说明](#52-纸型说明)

1. 通过**进纸调节器按钮**，调整打印机的默认纸型。如果你的打印机没有这个类似的按钮，可询问客服具体调节方法。

2. 调整打印模板，在程序里设置打印纸型

#### 4.2. 具体实现方法

> 基于上述 Demo，主要作如下修改：

```JavaScript

…略…

LODOP = getLodop();
LODOP.PRINT_INITA(0,10,"24.1cm","13.9cm","");
LODOP.SET_PRINT_PAGESIZE(1,"24.1cm","13.9cm","CreateCustomPage");
LODOP.SET_PRINT_MODE("CREATE_CUSTOM_PAGE_NAME","fyd_print_1");
// LODOP.SET_PRINT_MODE("POS_BASEON_PAPER",true);
// LODOP.SET_PREVIEW_WINDOW(1,0,0,1000,600,""); // 初始预览窗口大小
// LODOP.SET_SHOW_MODE("LANDSCAPE_DEFROTATED",1); // 横向打印时正向显示
LODOP.SET_PRINT_MODE("AUTO_CLOSE_PREWINDOW",1); // 打印后自动关闭预览
LODOP.SET_PRINT_MODE("CUSTOM_TASK_NAME","发运单打印"); // 打印队列中的文档名
LODOP.SET_SHOW_MODE("HIDE_PAPER_BOARD",1); // 去除背景滚动线

…略…

```

⚠️ 注意：**对于打印模板的调整，可使用 Lodop 打印设计功能，或一点点打印预览进行调节**。


### 5. 附录

#### 5.1. 相关常见问题

- [如何避免Lodop本地配置影响](http://www.c-lodop.com/faq/pp9.html)
- [打印位置不同，偏移量问题](http://www.c-lodop.com/faq/pp17.html)

#### 5.2. 纸型说明

![预览图片）](./paper1.jpg)

![预览图片）](./paper2.jpg)
