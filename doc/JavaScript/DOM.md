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