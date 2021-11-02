## 暗锚
1. 需求背景当：
   1. nav fixed定位在最顶端，nav-item使用的a标签，通过锚点实现 点击nav-item跳转对应楼层
   2. fixed定位完全脱离文档流，导致锚点跳转时 楼层部分内容会被nav覆盖，被覆盖楼层的高度 与nav高度相同
2. 解决方案：
   1. 在需要跳转到的 标签容器 中加上一个暗锚，并定位到距离顶端的top负距离值（nav高度），点击nav-item跳转对应楼层定位到暗锚时，就会自动空出一段距离了。
3. 关键代码
```javascript
<style>
    .nav {
        position: fixed;
        top: 0;
        height: 80px;
    }
    .hiddenHash {
        position: relative;
        top: -80px;
    }
</style>

<body>
    <!-- nav -->
    <ul class="nav">
        <li><a href="#first">第一</a></li>
        <li><a href="#second">第二</a></li>
        <li><a href="#third">第三</a>></li>
    </ul>

    <!-- 楼层 -->
    <div class="main">
        <!-- 注：跳转锚点承载方式：1）a标签name属性；2）其他标签id属性 -->
        <a name="first" class="hiddenHash"></a>第一内容
    </div>
    <div class="main">
        <a name="second" class="hiddenHash"></a>第二内容
    </div>
    <div class="main">
        <a name="third" class="hiddenHash"></a>第三内容
    </div>
</body>
```

## ES6 模版字符串中 使用if{}else{}条件判断语句
1. 解决方案：使用IIFE（Immediately-Invoked Function Expression 立即调用函数表达式）
2. 注意事项：
   1. 结果字符串 作为return的值返回
   2. 如果return的是一个动态数据，记得使用``，如果使用''会被直接输出为字符串
3. 代码如下
```javascript
const html = `<ul>
                <li>1</li>
                <li>2</li>
                <li>3</li>
                <li>
                    ${
                        (function () {
                            if (XXXXXXXXX) {
                                return `动态数据`;
                            } else {
                                return '静态数据';
                            }
                        })()
                    }
                </li>
            </ul>`
```


