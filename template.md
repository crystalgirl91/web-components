template标签用来定义网页中某些重复出现的部分的代码模板。它存在于DOM之中，默认浏览器是不会渲染此标签的内容的,只有当你真正用的时候才会去render。 

下面是一个模板的例子：
    <template id="template">
      <div class="profile">
        <img src="" class="profileImg">
        <div class="profile_name"></div>
      </div>
    </template>
  使用这个模板的时候，需要用javascript获取并操作template的内容然后插入DOM文档中。
  
      var temp = document.querySelector("#template");
      temp.querySelector(".profileImg").src="profile.jpg";
      temp.querySelector(".profile_name").innerHTML = "profile_name";
      document.body.appendChild(temp.content);
  
  上面的例子，直接将template.content插入DOM中，这样在一次插入操作后template的content就会丢失，这个模板就不可再重用
  .更好的做法是克隆模板节点，然后将克隆的副本插入DOM，这样就可以重用模板。如下：
  
      var temp = document.querySelector("#template");
      temp.querySelector(".profileImg").src="profile.jpg";
      temp.querySelector(".profile_name").innerHTML = "profile_name";
           document.body.appendChild(document.importNode(temp.content,true));
      或者:document.body.appendChild(temp.content.cloneNode(true));
      
  这里的importNode方法用于克隆外部文档的DOM节点，document.importNode方法接受两个参数，第一个参数是外部文档DOM节点，
  第二个参数是布尔值，表示是否克隆该节点的子节点，默认为FALSE，即不克隆子节点。cloneNode方法与importNode方法等效。
  
上面的代码就是往body里插入模板里的内容,这里要注意下,想要获取模板内的内容,得使用模板元素的content属性,内容的类型是documentFragment，一般在同时插入多个html内容的时候，用documentFragment是最有效率的, 这里还要注意下，假如直接把content的内容直接插入到目标元素内之后，模板的内容就会丢失，所以为了保证别的目标元素也想插入这个模板的话，可以使用Node的cloneNode方法，这是所有html节点都有的方法,参数传递true的话会深度clone.

用 <template> 来包裹内容为我们提供了几个重要属性。

*   它的内容在激活之前一直处于惰性状态。本质上，这些标记就是隐藏的 DOM，它们不会被渲染。

*   处于模板中的内容不会有副作用。脚本不会运行，图片不会加载，音频不会播放，...直到模板被使用。

*   内容不在文档中。在主页面使用 document.getElementById() 或 querySelector() 不会返回模板的子节点。

模板能够被放置在任何位置，包括 <head>，<body>，或 <frameset>，并且任何能够出现在以上元素中的内容都可以放到模板中。 注意，"任何位置"意味着 <template> 能够安全的出现在 HTML 解析器不允许出现的位置...几乎可以作为任何内容模型的子节点。 它也可以作为 <table> 或 <select> 的子元素
  
