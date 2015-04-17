长久以来，网页可以加载外部的样式表、脚本、图片、多媒体，却无法方便地加载其他网页，
iframe和ajax都只能提供部分的解决方案，且有很大的局限。HTML Import就是为了解决加载外部网页这个问题，而提出来的。

HTML Import用于将外部的HTML文档加载进当前文档。我们可以将组件的HTML、CSS、JavaScript封装在一个文件里，
然后使用下面的代码插入需要使用该组件的网页
        <link rel="import" href="dialog.html">
