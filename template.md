template标签用来定义网页中某些重复出现的部分的代码模板。它存在于DOM之中，但是在页面加载的时候是不可见的。
可以通过JS的DOM操作来控制template的内容。 

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
  
  上面的例子，直接将template.content插入DOM中，这样在一次插入操作后template的content就为空了，这个模板就不可再重用
  .更好的做法是克隆模板节点，然后将克隆的副本插入DOM，这样就可以重用模板。如下：
  
      var temp = document.querySelector("#template");
      temp.querySelector(".profileImg").src="profile.jpg";
      temp.querySelector(".profile_name").innerHTML = "profile_name";
           document.body.appendChild(document.importNode(temp.content,true));
      或者:document.body.appendChild(temp.content.cloneNode(true));
      
  这里的importNode方法用于克隆外部文档的DOM节点，document.importNode方法接受两个参数，第一个参数是外部文档DOM节点，
  第二个参数是布尔值，表示是否克隆该节点的子节点，默认为FALSE，即不克隆子节点。cloneNode方法与importNode方法等效。
  
  template.content是一个文档碎片节点（DOCUMENT_FRAGMENT_NODE）,与document.createDocumentFragment所创建的节点一样，
  都是以DocumentFragment方法为构造函数。
  
