动画引擎movy.js
===========================

movy 动画引擎是由B站UP主：奇乐编程学院 开发，项目发布在github上。

https://space.bilibili.com/372313671
https://github.com/rossning92/movy

movy 环境部署
++++++++++++++++

| 部署 movy 需要本机  node.js (version >= 12) 
| 使用命令 `npm i -g movy` 安装
| 然后使用 movy 命令打开实例列表

movy 动画编写
++++++++++++++++

创建一个新的 hello.js 文件::

    import * as mo from "movy";

    mo.addText("Hello, Movy!", {
    scale: 0.8,
    color: "yellow",
    }).grow();

movy 动画生成
++++++++++++++++

命令行输入 `movy hello.js` 会自动打开浏览器，显示动画。

在界面点击 render 按钮渲染为视频进行下载。


