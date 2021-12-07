# event事件对象
## event.target 和 event.currentTarget的区别
1. event.currentTarget 会返回**当前触发事件元素**，event.target会返回**触发事件的源头元素**
2. event.currentTarget 在控制台展开查看的时候已经不存在了。如果想拿到它，可以使用变量进行缓存，然后再进行操作

```
    <ul>
        <li>1</li>
        <li>2</li>
        <li class="ok">3</li>
    </ul>
    <script>
        document.querySelector('.ok').addEventListener('click', function (event) {
            console.log('event', event); // 展开后发现 event.currentTarget 值为null
            console.log('event.currentTarget', event.currentTarget); // 值正常
        });
    </script>
```

## addEventListener方法的第三个参数
1. 给HTML元素绑定事件有下面三种方法，以最常见的“click”事件为例
    1. 直接在对应的HTML元素标签上绑定函数，违反了HTML与JavaScript分离的准则，不推荐
        ```html
            <button id='submit' onclick='onClickFn()'>Click Me!</button>
        ```
    2. 在JS代码中指定元素的“onclick”方法，只能给一个事件绑定一个响应函数，重复绑定会覆盖之前的绑定
        ```javascript
            var btn = document.getElementById("submit");
            btn.onclick = onClickFn;
        ```
    3. 使用事件监听“addEventListener”绑定方法，可以绑定多个不同的函数，**不会覆盖**，推荐
        ```javascript
            var btn = document.getElementById("submit");
            btn.addEventListener("click", onClickFn, false);
        ```
2. 第三种方法“addEventListener”中的第三个参数是用来控制什么的呢
   1. 事件捕获 和 事件冒泡
      1. 还是以最常见的“click”事件为例，页面中标签由里到外层层嵌套 结构如同洋葱，当鼠标点击所看到的的按钮时，其实发生了一系列的事件传递：button实际上是被body“包裹”起来的，body是被html“包裹”起来的，html又是被document“包裹”起来的，document是被window“包裹”起来的。所以，在点击鼠标的时候，最先获得这个点击的是最外面的window，然后经过一系列传递 才会传到最后的目标button，当传到button的时候，这个事件又会像水底的泡泡一样慢慢往外层穿出，直到window结束。
      2. 综上，一个事件的传递过程包含三个阶段，分别称为：
         1. 捕获阶段
         2. 目标阶段
         3. 冒泡阶段
            1. 其中目标指的就是 包裹得最深的那个元素
   2.  “addEventListener”第三个参数是用来控制事件处理程序 是事件捕获时触发 or 事件冒泡时触发
       1.  addEventListener的第三个参数设置为true和false的区别
           1.  true表示该元素在事件的“捕获阶段”（由外往内传递时）响应事件；
           2.  false表示该元素在事件的“冒泡阶段”（由内向外传递时）响应时间
            ```html
    `               <div id='d'>
                    <p id='p'>
                        <span id='s'>Click Me!</span>
                    </p>
                </div>
                <script>
                    var div = document.getElementById('d');
                    var p = document.getElementById('p');
                    var span = document.getElementById('s');

                    function onClickFn (event) {
                        var tagName = event.currentTarget.tagName;
                        var phase = event.eventPhase;
                        console.log(tagName, phase);
                    }

                    div.addEventListener('click', onClickFn, false);
                    p.addEventListener('click', onClickFn, false);
                </script>
            ```
                1. 点击“Click Me!”，即可在控制台看到如下结果：
                    ```
                        P 3
                        DIV 3 // “3”和“冒泡阶段”对应
                    ```
                2. p和div都是在冒泡阶段相应了事件，由于冒泡的特性，裹在里层的p率先做出响应，如果把上面代码里面中addEventListener的第三个参数设置为true，那么运行的结果如下：
                    ```
                        DIV 1
                        P 1
                    ```



至此，你可能会有疑问，还有一个“目标阶段”呢？

您不妨给span元素绑定事件，自己测试一下。





在冒泡阶段，如果不希望事件继续往上传播，例如，冒泡的p的时候就停止传播，那么，可以在p的事件回调函数里面这么写：

function onClickFn (event) {
    // code here
    event.stopPropagation();
}
这样，冒泡到p的时候，就不会再向上传播了，即，div不会收到冒泡上来的click事件。

如果还想把其它与p绑定的响应函数的事件也“屏蔽”掉，需要把stopPropagation换为stopImmediatePropagation。

