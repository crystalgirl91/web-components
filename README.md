# web-components

网站开发中往往需要一些可重用的模块，比如日历，调色板等。这种模块就被称为“组件”（component）。

Web component就是开发web组件的一系列技术规范的组合，它包括HTML template，custom Element ,shadow DOM, HTML import.
使用时这四者不一定都要采用，可以任意搭配使用。
采用组件进行网站开发有利于代码的管理和使用。

优点：

1.  管理和使用非常容易。加载和卸载组件，往往只需要删除后添加一行代码，例如以下代码定义了一个对话框组件。
  
      <link href="my-dialog.html" rel="import">
      <my-dialog heading="dialog">dialog dialog</my-dialog>

2.  组件是模块化编程的体现，有利于代码的重用，标准格式的模块，可以跨平台、跨框架使用，构建、部署和与其他UI元素互动都有统一做法
3.  组件提供了HTML,CSS,JAVASCRIPT封装的方法，可以隔离同一页面上的其他代码，
    使得组件的样式及事件与页面的样式事件相互独立，互不影响
