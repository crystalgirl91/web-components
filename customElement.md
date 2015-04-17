#Custom Element

自定义元素是一个可由创建者来自定义接口的对象。在创建时我们需要通过 document.registerElement()来对自定义元素进行注册。
该方法会返回一个元素的构造器，
通过该构造器我们就可以创建我们的自定义元素的实例了。

    var MyButton= document.registerElement('my-button');
    document.body.appendChild(new MyButton());
    
实际上 document.registerElement(tag-name, prototype) 包含两个参数：

*  tag-name: 自定义元素的标签名，这个标签名必须包含连字符’-’，这样做的母的是用以区分自定义元素和HTML规范的元素。

*  prototype: 这是一个可选的参数，用于描述该元素的原型，在该元素中你可以为自定义元素进行接口的定义。

-----------------------------

    var MyElement = document.registerElement('my-element', { 
      prototype: Object.create(HTMLElement.prototype, { 
          createdCallback: { 
              value: function() { 
                  this.innerHTML = "<p>I'm a Custom Element</p>"
              } 
          } 
      }) 
    });
    document.body.appendChild(new MyElement())
    
-----------------------------
      
在上面的例子中，我们通过Object.create()方法创建了一个继承自HTMLElement的对象作为自定义对象的原型，
并设置了元素默认的 innerHTML ，如果你对Object.create()方法的第二个参数不熟悉，你最好先去查阅一下。
实际上它的上面的例子跟下面给出的写法的效果是一样的：

-----------------------------

      var MyElementProto = Object.create(HTMLElement.prototype)
      
      MyElementProto.createdCallback = function() {
          this.innerHTML = "<p>I'm a Custom Element</p>"
      }
      
      var MyElement = document.registerElement('my-element', { prototype: MyElementProto })
      
      document.body.appendChild(new MyElement())
      
-----------------------------
      
接着，在页面上我们可以看到渲染出如下结构：

-----------------------------

      <my-element>
          <p>I'm a Custom Element</p>
      </my-element>
-----------------------------

##自定义元素的生命周

在上面的例子中我们可以看到自定义元素的原型上有一个createdCallback 属性，它的值是一个回调函数，
在自定义元素被创建的时候被调用。实际上自定义元素在它的生命周期中可能会经历以下几种变化：

* 自定义元素在其注册前被创建
* 自定义元素被注册
* 自定义元素的实例在自定义元素注册后被创建
* 自定义元素被插入到文档中
* 自定义元素从文档中移除
* 自定义元素的属性被创建、移除、修改

在自定义元素经历上面某些变化时，不同的回调函数会被调用。这些回调函数被保存在一个名为生命周期回调的键值对集合中。
我们可实现的回调函数总共有以下4种，其中attributeChangedCallback 的回调函数中我们可以通过其参数访问到
操作的属性名、老的属性值、新的属性值。

* createdCallback :自定义元素的实例被创建时调用
* attachedCallback:自定义元素的实例插入文档时调用
* detachedCallback:自定义元素的实例移除文档时调用
* attributeChangedCallback:自定义元素的实例属性发生变化时调用（添加，移除，修改）

  function(propertyName,oldValue,newValue){}
  
  属性添加时oldValue为null
  属性删除时newValue为null
  
###DOM

        <div id="modify">
            <label class="CEgreen"><input type="radio" name="CEclass" value="green">green box</label>
            <label class="CEred"><input type="radio" name="CEclass" value="red">red box</label>
        </div>
        
###JS

      var MyElement = document.registerElement('my-element', { 
        prototype: Object.create(HTMLElement.prototype, { 
          createdCallback: { 
            value: function() {
              this.innerHTML = "<span>I'm a Custom Element</span>"
            }
          },
          attributeChangedCallback: {
            value: function(property, oldValue, newValue) {
              this.innerHTML = "attribute '" + property + "' is modified to " + newValue
            }
          }
        }) 
      })
      document.body.appendChild(new MyElement())
      
      var temp = document.querySelector("#modify")
      var myElement = document.querySelector("my-element")
      
      temp.addEventListener('click', function(e){
        console.log(e.target.value)
        myElement.className = e.target.value
      })
