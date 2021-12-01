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

## 新东方大学事业部国庆、双11抽奖活动动效
- 使用css3 [animation](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)实现（本需求只用到了 animation-name、animation-duration、animation-timing-function 和 animation-iteration-count）
- animation: [animation-name/动画名称] [animation-duration/动画时间] [animation-timing-function/动画如何完成一个周期] [animation-delay/动画延时] [animation-iteration-count/动画播放次数] [animation-direction/指定是否应该轮流反向播放动画] [animation-fill-mode/规定当动画不播放时（当动画完成时，或当动画有一个延迟未开始播放时），要应用到元素的样式] [animation-fill-mode/指定动画是否正在运行或已暂停];
    - animation-timing-function取值
        -  linear [动画从头到尾的匀速]
        - ease [默认。动画以低速开始，然后加快，在结束前变慢]
        - ease-in [动画以低速开始]
        - ease-out [动画以低速结束]
        - ease-in-out [动画以低速开始和结束]
        - cubic-bezier(n,n,n,n) [在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值]
```javascript
<style>
    .wrap {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);  /* 等同于 transform: translateX(-50%) translateY(-50%); */
    }
    .container {
        position: relative;
        width: 510px;
        height: 340px;
        padding: 0;
        border: 1px solid black;
        border-radius: 50px;
        margin: 0;
        margin-bottom: 10px;
        list-style: none;
        overflow: hidden;
    }
    .ball {
        position: absolute;
        width: 95px;
        height: 95px;
        border-radius: 50%;
        text-align: center;
        line-height: 95px;
    }
    /* 红橙黄绿蓝靛紫 天蓝 黑棕金银粉*/
    .ball1 {
        top: 166px;
        left: 0px;
        background-color: red;
    }
    .ball2 {
        top: 153px;
        left: 72px;
        background-color: orange;
    }
    .ball3 {
        top: 170px;
        left: 155px;
        background-color: yellow;
    }
    .ball4 {
        top: 160px;
        left: 253px;
        background-color: green;
    }
    .ball5 {
        top: 110px;
        left: 280px;
        background-color: blue;
    }
    .ball6 {
        top: 175px;
        left: 323px;
        color: #fff;
        background-color: indigo;
    }
    .ball7 {
        top: 180px;
        left: 414px;
        background-color: skyblue;
    }
    .ball8 {
        top: 240px;
        left: 40px;
        background-color: black;
    }
    .ball9 {
        top: 250px;
        left: 120px;
        background-color: brown;
    }
    .ball10 {
        top: 245px;
        left: 200px;
        background-color: silver;
    }
    .ball11 {
        top: 250px;
        left: 275px;
        background-color: gold;
    }
    .ball12 {
        top: 250px;
        left: 360px;
        background-color: pink;
    }
    .ball-animation {
        animation-duration: 1.5s;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
    }
    .ball1-keyframes {
        animation-name: ball1Keyframes;
    }
    .ball2-keyframes {
        animation-name: ball2Keyframes;
    }
    .ball3-keyframes {
        animation-name: ball3Keyframes;
    }
    .ball4-keyframes {
        animation-name: ball4Keyframes;
    }
    .ball5-keyframes {
        animation-name: ball5Keyframes;
    }
    .ball6-keyframes {
        animation-name: ball6Keyframes;
    }
    .ball7-keyframes {
        animation-name: ball7Keyframes;
    }
    .ball8-keyframes {
        animation-name: ball8Keyframes;
    }
    .ball9-keyframes {
        animation-name: ball9Keyframes;
    }
    .ball10-keyframes {
        animation-name: ball10Keyframes;
    }
    .ball11-keyframes {
        animation-name: ball11Keyframes;
    }
    .ball12-keyframes {
        animation-name: ball12Keyframes;
    }

    /* 放开ul的overflow: hidden就会发现keyframes中ball的tanslate是随意写的 */
    @keyframes ball1Keyframes {
        0% {
            transform: translate(300px, 230px);
        }
        20% {
            transform: translate(200px, -100px);
        }
        40% {
            transform: translate(50px, 230px);
        }
        60% {
            transform: translate(300px, -50px);
        }
        80% {
            transform: translate(200px, 240px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball2Keyframes {
        0% {
            transform: translate(300px, -120px);
        }
        10% {
            transform: translate(250px, 130px);
        }
        30% {
            transform: translate(-50px, -120px);
        }
        50% {
            transform: translate(0px, 140px);
        }
        80% {
            transform: translate(300px, -180px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball3Keyframes {
        0% {
            transform: translate(70px, -290px);
        }
        25% {
            transform: translate(320px, 0px);
        }
        50% {
            transform: translate(-20px, -290px);
        }
        80% {
            transform: translate(290px, 0px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball4Keyframes {
        0% {
            transform: translate(50px, 250px);
        }
        12% {
            transform: translate(-150px, -30px);
        }
        30% {
            transform: translate(-140px, 260px);
        }
        60% {
            transform: translate(-10px, -30px);
        }
        80% {
            transform: translate(-20px, 260px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball5Keyframes {
        0% {
            transform: translate(-50px, -170px);
        }
        22% {
            transform: translate(150px, 145px);
        }
        46% {
            transform: translate(200px, -115px);
        }
        80% {
            transform: translate(-100px, 145px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball6Keyframes {
        0% {
            transform: translate(260px, 40px);
        }
        15% {
            transform: translate(-80px, -260px);
        }
        30% {
            transform: translate(-40px, 40px);
        }
        45% {
            transform: translate(100px, -290px);
        }
        60% {
            transform: translate(-80px, -280px);
        }
        75% {
            transform: translate(10px, 40px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball7Keyframes {
        0% {
            transform: translate(-60px, -170px);
        }
        20% {
            transform: translate(90px, 160px);
        }
        40% {
            transform: translate(-220px, -140px);
        }
        60% {
            transform: translate(160px, -60px);
        }
        80% {
            transform: translate(-100px, -100px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball8Keyframes {
        0% {
            transform: translate(140px, -120px);
        }
        20% {
            transform: translate(-140px, 40px);
        }
        40% {
            transform: translate(-180px, -240px);
        }
        60% {
            transform: translate(100px, 50px);
        }
        80% {
            transform: translate(-180px, -220px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball9Keyframes {
        0% {
            transform: translate(-300px, -180px);
        }
        30% {
            transform: translate(-350px, 120px);
        }
        60% {
            transform: translate(-100px, -200px);
        }
        80% {
            transform: translate(-200px, 100px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball10Keyframes {
        0% {
            transform: translate(-300px, -270px);
        }
        15% {
            transform: translate(20px, -220px);
        }
        30% {
            transform: translate(-350px, 10px);
        }
        50% {
            transform: translate(0px, -150px);
        }
        75% {
            transform: translate(-300px, -300px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }

    @keyframes ball11Keyframes {
        0% {
            transform: translate(-270px, -70px);
        }
        32% {
            transform: translate(-320px, 220px);
        }
        60% {
            transform: translate(10px, -10px);
        }
        80% {
            transform: translate(-260px, 220px);
        }
        100% {
            transform: translate(0px, 0px);
        }
    }
    @keyframes ball12Keyframes {
        0% {
            transform: translate(-370px, -70px);
        }
        32% {
            transform: translate(-120px, 220px);
        }
        60% {
            transform: translate(10px, -10px);
        }
        80% {
            transform: translate(-260px, 220px);
        }
        100% {
            transform: translate(0, 0);
        }
    }

</style>
<script src="https://code.jquery.com/jquery-1.12.4.min.js" integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=" crossorigin="anonymous"></script>
<body>
    <div class="wrap">
        <ul class="container">
            <li class="ball ball1">1</li>
            <li class="ball ball2">2</li>
            <li class="ball ball3">3</li>
            <li class="ball ball4">4</li>
            <li class="ball ball5">5</li>
            <li class="ball ball6">6</li>
            <li class="ball ball7">7</li>
            <li class="ball ball8">8</li>
            <li class="ball ball9">9</li>
            <li class="ball ball10">10</li>
            <li class="ball ball11">11</li>
            <li class="ball ball12">12</li>
        </ul>
        <button id="blBtn">begin lottery</button>
        <button id="slBtn">stop lottery</button>
    </div>
    <script>
        $("#blBtn").click(function() {
            $(".ball").each((index, item) => {
                $(item).addClass(`ball-animation ball${index+1}-keyframes`);
            });
        });
        $("#slBtn").click(function() {
            $(".ball").each((index, item) => {
                $(item).removeClass(`ball-animation ball${index+1}-keyframes`);
            });
        });
    </script>
</body>
```


## event.target 和 event.currentTarget [传送门](https://juejin.cn/post/6844903506399199246)
1. currentTarget始终是监听事件者，而target是事件的真正发出者
2. this、currentTarget和target
   1. 在事件处理程序内部，this始终全等于currentTarget的值
   2. 如果直接将事件处理程序是被注册在 目标元素上，则this、currentTarget和target三者的值全等
3. 在W3C模型中，任何事件发生时，先从顶层开始进行事件捕获，直到事件触发到达了事件源元素，即事件捕获（事件的传递过程）；然后，该事件会随着DOM树的层级路径，由子节点向父节点进行层层传递，直至到达document，即事件冒泡（事件的响应过程）
4. 事件委托
   1. 事件委托就是利用事件冒泡机制，指定一个事件处理程序，来管理某一类型的所有事件
      1. 帮助理解的生活场景：公司的员工们经常会收到快递。为了方便签收快递，有两种办法：一种是快递到了之后收件人各自去拿快递；另一种是委托前台MM代为签收。很显然，第二种方案更为方便高效，同时这种方案还有一种优势，那就是即使有新员工入职，前台的MM都可以代替新员工签收快递
   2. 为什么要用事件委托
      1. 例举个场景：ul中包含n个li，要给每个li注册相同click处理程序，如果单独去给每个li注册事件，需要获取n次dom元素、注册多个事件处理程序（js函数），这两点将引发重绘和重排、增加内存占用，直接影响到页面的整体运行性能；而使用事件委托，只需要给ul元素注册事件


## 前端模块规范（共三种）：CommonJs、AMD 和 [CMD](https://www.jianshu.com/p/ebdf2233e3fe) [传送门](https://www.jianshu.com/p/d67bc79976e6)
1. CommonJs 是服务器端模块的规范，由Node推广使用
   1. 加载模块使用require方法，该方法读取一个文件并执行，返回文件内部的module.exports对象，require 是同步的。模块系统需要同步读取模块文件内容，并编译执行以得到模块接口；然而在浏览器端，加载 JavaScript 最佳、最容易的方式是在 document 中插入 script标签。但脚本标签天生异步，传统 CommonJS 模块在浏览器环境中无法正常加载  
    ```javascript
    math.js
    exports.add = function() {
        var sum = 0, i = 0, args = arguments, l = args.length;
        while (i < l) {
        sum += args[i++];
        }
        return sum;
    };

    increment.js
    var add = require('math').add;
    exports.increment = function(val) {
        return add(val, 1);
    };

    index.js
    var increment = require('increment').increment;
    var a = increment(1); //2
    ```
2. AMD 是 RequireJS 在推广过程中对模块定义的规范化产出
   1. AMD是 "Asynchronous Module Definition"的缩写，意为"异步模块定义"，依赖关系前置,在定义模块的时候就要声明其依赖的模块
    ```javascript
    define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
        a.doSomething()
        // 此处略去 100 行
        b.doSomething()
        ...
    })
    ```
3. CMD 是 SeaJS 在推广过程中对模块定义的规范化产出
   1. CMD 是 “Common Module Definition”的缩写，意为"通用模块定义"，按需加载依赖,只有在用到某个模块的时候再去require
    ```javascript
    define(function(require, exports, module) {
        var a = require('./a')
        a.doSomething()
        // 此处略去 100 行
        var b = require('./b') // 依赖可以就近书写
        b.doSomething()
        // ... 
    })
    ```

### 硬编码
1. 背景：前端中通常会出现一些 涉及业务方面的固定值，有些时候是通过常量被直接写死在逻辑代码中的，虽然从短期来看确实解决了交付代码的压力；但是从长期来看，这样的编码方式并不适应业务需求的变更，不够灵活
2. 何谓硬编码：最简单、最直接的理解就是将一些在代码运行之前就确定好了的、可以变化的固定值写死在代码中，后续若想更改的话，只能是重新修改源代码和重新编译、构建后才会生效，这种编码过程就是硬编码。网络的解释是这样的：硬编码是将数据直接嵌入到程序或其他可执行对象的源代码中的软件开发实践，与从外部获取数据或在运行时生成数据不同
   1. e.g. 新东方大学事业部 国庆、双11抽奖活动中的 活动id、添加收获地址跳转链接等值都是通过常量的方式定义在代码中的
3. 解决方案：涉及业务方面的固定值 可以 通过调用接口获取 || 构建后作为静态资源存放于服务端代码中的 也可以通过资源配置文件从服务端读取（苏宁礼遇wap）

### 如何声明一个 包含换行的 String变量 --> 适用ES6字符串模版
```javascript
    const str1 = '1
        2
        3'; // Uncaught SyntaxError: Invalid or unexpected token
    const str2 = `1
        2
        3`;
    console.log(str2);;; // '1\n2\n3'
```

### 电梯导航
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{margin: 0; padding: 0;}
        .nav-container {
            position: fixed;
            left: 0;
            top: 20%;
            width: 50px;
        }
        .nav-item {
            box-sizing:  border-box;
            width: 50px;
            height: 50px;
            text-align: center;
            line-height: 50px;
            color: #FFF;
            cursor: pointer;
        }
        .nav-item.active {
            border: 2px solid #FFF;
        }
        .header {
            width: 100%;
            height: 300px;
            margin-bottom: 20px;
            background: hotpink;
        }
        .floor {
            width: 100%;
            height: 400px;
            margin-bottom: 20px;
        }
        .footer {
            width: 100%;
            height: 300px;
            background: hotpink;
        }
    </style>
</head>
<body>
    <ul class="nav-container">
        <li class="nav-item active">1</li>
        <li class="nav-item">2</li>
        <li class="nav-item">3</li>
        <li class="nav-item">4</li>
        <li class="nav-item">5</li>
        <li class="nav-item">6</li>
        <li class="nav-item">7</li>
    </ul>
    
    <div class="header"></div>
    <div class="floor floor-01"></div>
    <div class="floor floor-02"></div>
    <div class="floor floor-03"></div>
    <div class="floor floor-04"></div>
    <div class="floor floor-05"></div>
    <div class="floor floor-06"></div>
    <div class="floor floor-07"></div>
    <div class="footer"></div>

    <script src="https://code.jquery.com/jquery-1.12.4.min.js" integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=" crossorigin="anonymous"></script>
    <script>
        $(function(){
            //给导航 和 楼层上色：红橙黄绿蓝靛紫
            const colorArr = ['red','orange','yellow','green','blue','cyan','purple'];
            for(i = 0; i < colorArr.length; i++){
                $('.nav-item').eq(i).css({background: colorArr[i]});
                $('.floor').eq(i).css({background: colorArr[i]});
            }

            //获取各个楼层的距离 页面最顶部 的垂直偏移量,并放入数组
            const floorOffsetTopArr = [];
            for(var i = 0; i < $('.floor').length; i++){
                floorOffsetTopArr.push($('.floor').eq(i).offset().top);
            }
                
            //给导航每个栏目按钮添加点击事件，点击导航上的每个栏目按钮，html(body)滑动到对应的栏目
            $('.nav-item').click(function(){
                // css中没有scrollTop属性，scrollTop是jQuery中的方法
                // animate 与 scrollTop 结合使用达成滑动回顶部效果
                $('html,body').animate({scrollTop: `${floorOffsetTopArr[$(this).index()] - 320}px`});
                $(this).addClass('active').siblings().removeClass('active');
            });

            function highlightNavItem() {
                // 获取获取页面 当前已经滚动的 scrollTop值 
                const windScrollTop = $(window).scrollTop();
                // 遍历每一个楼层 或者 每个楼层对应的按钮
                for(i = 0; i < $('.floor').length; i++){
                    // 滚动到最后一个floor之前
                    if(windScrollTop < floorOffsetTopArr[floorOffsetTopArr.length-1]){
                        // 给一个循环动态判断的条件，若当前scrollTop值大于数组的arr[i],且小于arr[i+1],就对应的栏目按钮添加样式
                        if(windScrollTop >= (floorOffsetTopArr[i] - 320) && windScrollTop < (floorOffsetTopArr[i+1] - 320)){
                            $('.nav-item').eq(i).addClass('active').siblings().removeClass('active');
                        }
                    }else{
                        // 滚动到最后一个floor
                        $('.nav-item').eq(floorOffsetTopArr.length-1).addClass('active').siblings().removeClass('active');
                    }
                }
            }

            highlightNavItem(); // 页面进入时就执行一次，适用滚动到中间位置 刷新页面高亮对应nav-item的场景
            
            //给window添加滚动事件
            $(window).scroll(function(){
                highlightNavItem();
            });
        });
    </script>
</body>
</html>
```

### DOM事件绑定 与 箭头函数
- DOM事件绑定中，如果回调函数中使用了 this 来获取当前注册的DOM元素（事件源），那么回调函数就不能使用剪头函数，因为箭头函数中 this 会向函数的上一层查找

### 页面有H5、PC双端，两者的访问链接不同：在移动端打开PC链接 自动跳转至 H5链接，在PC端打开H5链接 自动跳转至 PC链接
- 两者用“!“可以相互转化，检索全网 答案也是参差不齐，以下代码片段摘自 实际上线项目，笔记就以实际上线项目的代码为准吧
- PC
```javascript
(function () {
    var sUserAgent = navigator.userAgent.toLowerCase();
    var bIsIpad = sUserAgent.match(/ipad/i) == "ipad";
    var bIsIphoneOs = sUserAgent.match(/iphone os/i) == "iphone os";
    var bIsMidp = sUserAgent.match(/midp/i) == "midp";
    var bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i) == "rv:1.2.3.4";
    var bIsUc = sUserAgent.match(/ucweb/i) == "ucweb";
    var bIsAndroid = sUserAgent.match(/android/i) == "android";
    var bIsCE = sUserAgent.match(/windows ce/i) == "windows ce";
    var bIsWM = sUserAgent.match(/windows mobile/i) == "windows mobile";
    if (bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM) {
        location.href = `${H5访问链接}`;
    }
})();
```
- H5
```javascript
(function () {
    if (!navigator.userAgent.match(
            /(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i
        )
    ) {
        location.href = `${PC访问链接}`;
    }
})();

```

### CSS媒体查询
1. CSS2
   1. 既然CSS2可以实现媒体查询 那为什么不用这个方法呢，CSS2媒体查询最大的弊端就是它会增加页面http的请求次数，增加了页面负担，我们用CSS3把 媒体查询样式 都写在一个文件里面才是最佳的方法
```html
<link rel="stylesheet" href="styleA.css" media="screen and (min-width: 800px)">  
<link rel="stylesheet" href="styleB.css" media="screen and (min-width: 600px) and (max-width: 800px)">  
<link rel="stylesheet" href="styleC.css" media="screen and (max-width: 600px)">  
```
   2. 上面将设备分成3种，分别是宽度大于800px时，应用 styleA ，宽度在600px到800px之间时应用 styleB ，以及宽度小于600px时应用 styleC 。那假如宽度正好等于800px时该应用那个样式？是 styleB，因为前两条表达式都成立，按CSS默认优先级规则后者覆盖了前者。
因此，为了避免冲突，这个例子正常情况应该这样写：
```html
<link rel="stylesheet" href="styleA.css" media="screen">  
<link rel="stylesheet" href="styleB.css" media="screen and (max-width: 800px)">  
<link rel="stylesheet" href="styleC.css" media="screen and (max-width: 600px)">  
```
2. CSS3
   1. 加入meta标签
    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    ```
      1. width=device-width：宽度等于当前设备的宽度
      2. initial-scale：初始的缩放比例（默认设置为1.0）
      3. minimum-scale：允许用户缩放到的最小比例（默认设置为1.0）
      4. maximum-scale：允许用户缩放到的最大比例（默认设置为1.0）
      5. user-scalable：用户是否可以手动缩放（默认设置为no，因为我们不希望用户放大缩小页面）
   2. 语法：@media mediatype and | not | only (media feature) { css-code; }
      1. mediatype取值（目前项目中最常使用到的还是 screen）
         1. all 所有媒体
         2. braille 盲文触觉设备
         3. embossed 盲文打印机
         4. print 手持设备
         5. projection 打印预览
         6. screen 彩屏设备
         7. speech '听觉'类似的媒体类型
         8. tty 不适用像素的设备
         9. tv 电视
      2. 关键字
         1. and
         2. not：用来排除某种制定的媒体类型
         3. only：用来定某种特定的媒体类型
```css
// styleA.css代码
@media screen and (max-width: 800px){ 
    // styleB.css代码
}
@media screen and (max-width: 600px){ 
    // styleC.css代码
}
```

### 页面TDK
```html
<title>title</title>
<meta name="description" content="page's description"/>
<meta name="keywords" content="keyword1,keyword2,keyword3" />
```
1. title
   1. title，就是浏览器标签上显示的内容，不仅用户能看到，也能被搜索引擎检索到（搜索引擎在抓取网页时，最先读取的就是网页标题，所以title是否正确设置极其重要。）title一般不超过80个字符，而且词语间要用英文“-”隔开，因为计算机只对英语的敏感性较高，对汉语的敏感性不高
2. description
   1. description，和上面的keywords一样，是用户不查看源代码看不到的，而且也是对于一个网页的简要内容概况。不同的是，keywords是由几个词语的组成的，而description则是完整的一句话。description一般不超过150个字符，描述内容要和页面内容相关
3. keywords
   1. keywords，是用户不查看源代码看不到的。主要作用是告诉搜索引擎本页内容是围绕哪些词展开的。因此keywords的每个词都要能在内容中找到相应匹配，才有利于排名。keywords一般不超过3个，每个关键词不宜过长，而且词语间要用英文“,”隔开。为什么用英文上文已经说过。而且，尽量将重要的关键字靠前放，因为靠后的关键字排名较差，除非你站有很高的权重
4. 结：TDK名义上要使用英文，但我查看了下国内知名电商网站 jd、taobao 也都是使用的中文，so 入乡随俗吧
- jd PC官网TDK
```html
<title>京东(JD.COM)-正品低价、品质保障、配送及时、轻松购物！</title>
<meta name="description" content="京东JD.COM-专业的综合网上购物商城，为您提供正品低价的购物选择、优质便捷的服务体验。商品来自全球数十万品牌商家，囊括家电、手机、电脑、服装、居家、母婴、美妆、个护、食品、生鲜等丰富品类，满足各种购物需求。">
<meta name="Keywords" content="网上购物,网上商城,家电,手机,电脑,服装,居家,母婴,美妆,个护,食品,生鲜,京东">
```
- taobao PC官网TDK
```html
  <title>淘宝网 - 淘！我喜欢</title>
  <meta name="description" content="淘宝网 - 亚洲较大的网上交易平台，提供各类服饰、美容、家居、数码、话费/点卡充值… 数亿优质商品，同时提供担保交易(先收货后付款)等安全交易保障服务，并由商家提供退货承诺、破损补寄等消费者保障服务，让你安心享受网上购物乐趣！">
  <meta name="keywords" content="淘宝,掏宝,网上购物,C2C,在线交易,交易市场,网上交易,交易市场,网上买,网上卖,购物网站,团购,网上贸易,安全购物,电子商务,放心买,供应,买卖信息,网店,一口价,拍卖,网上开店,网络购物,打折,免费开店,网购,频道,店铺">
```

### css适配iPhoneX屏幕安全区（后来fixed底部导航并未做iphoneX以上机型安全区处理，之前电商项目有处理但并未看细节，相当于此点并进行过未实战）
1. 场景：iPhoneX对比起以前其他的手机，屏幕顶部变成了留海屏，底部取消了物理按键改成了小黑条，这种改动导致了web开发中页面上新的适配问题。比如一些需要贴在底部的按钮，和呼起的tabBar和底部弹出框，在iphoneX上就会出现被小黑条遮挡内容，或者页面上出现白色空隙的问题
2. viewport-fit：iOS11 新增特性，苹果公司为了适配 iPhoneX 对现有 viewport meta 标签的一个扩展，用于设置网页在可视窗口的布局方式，可设置三个值：
   1. contain: 可视窗口完全包含网页内容（左图）
   2. cover：网页内容完全覆盖可视窗口（右图）![viewportFit][viewportFitPic]
   3. auto：默认值，跟 contain 表现一致
3. env：iOS11 新增特性，Webkit 的一个 CSS 函数，用于向 CSS 插入用户代理定义的变量设定安全区域与边界的距离，有四个预定义的变量：
   1. safe-area-inset-left：安全区域距离左边边界距离
   2. safe-area-inset-right：安全区域距离右边边界距离
   3. safe-area-inset-top：安全区域距离顶部边界距离
   4. safe-area-inset-bottom：安全区域距离底部边界距离
   5. 注意：env()必须配合 viewport-fit=cover 使用，我们最常用的就是 safe-area-inset-bottom, 这个代表着不被小黑条遮挡的安全距离
```html
<meta content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=0,viewport-fit=cover" name="viewport"/>
```
```css
/* 贴底元素 */
.container 
  position: absolute;
  bottom: 0;
  padding-bottom: constant(safe-area-inset-bottom); /* 兼容 iOS < 11.2 */
  padding-bottom: env(safe-area-inset-bottom); /* 兼容 iOS >= 11.2 */
  ...
}
```

### 移动开发的HTML5页面点击按钮出现闪烁或黑色背景解决方案
1. 场景：节日活动推广落地页面，PC、wap双端，页面仅有一些点击效果相似的按钮 基本没有其他交互，时间紧张 为尽快上线，协调UI将设计稿切分成一块儿块儿的图片，前端用div布局 用css将展示内容作为背景图进行设置，涉及到 点击按钮 的部分，前端使用相同 宽、高、圆角的无边框、透明div进行定位覆盖，点击事件绑定在 覆盖在按钮的div上：pc浏览器模拟移动端仿真模式 || 真机上 点击按钮（div）出现闪烁 或 黑色背景
   1. pc: https://nce.koolearn.com/zhuanti/oral_pc
   2. wap: https://nce.koolearn.com/zhuanti/oral_wap
2. 解决方案
   1. 设置html || * 的 -webkit-tap-highlight-color样式
       1. -webkit-tap-highlight-color 是一个没有标准化的属性，能够设置点击元素 || 链接时出现的高亮颜色。显示给用户的高光是他们成功点击的标识，以暗示他们点击的元素
       2.  浏览器兼容：webkit/safari, Blink/Chrome
       3.  随意查阅了下m.jd.com || m.taobao.com网站css，都有对“-webkit-tap-highlight-color”的设置
   ```css
    *{
        -webkit-tap-highlight-color: transparent;
    }
    ```

### jQuery常用api
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        ul {
            list-style: none;
        }
        li {
            width: 500px;
            height: 50px;
        }
        .box01 {
            background-color: red;
        }
        .box02 {
            background-color: orange;
        }
        .box03 {
            background-color: yellow;
        }
        .box04 {
            background-color: green;
        }
    </style>
</head>
<body>
    <ul>
        <li class="box01"></li>
        <li class="box02"></li>
        <li class="box03"></li>
        <li class="box04"></li>
    </ul>
    <script src="https://code.jquery.com/jquery-1.12.4.min.js" integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=" crossorigin="anonymous"></script>
    <script>
    // jQuery 事件绑定 || 事件委托方式：多个元素绑定相同事件、同时绑定多个事件
        // 多个事件源之间使用“,”分割，多个事件之间使用" "分割
        // 事件绑定
        $(".box01, .box02").on("click mouseover", function(event) {
            console.log(`事件绑定：${event.target.className} 的 ${event.type} 事件触发了`);
        });
        // 事件委托
        $("body").on("click mouseover", ".box03, .box04", function(e) {
            console.log(`事件委托：${event.target.className} 的 ${event.type} 事件触发了`);
        });

    // jQuery 判断元素上是否包含某个class
        $("li").on("mouseover", function() {
            if ($(this).hasClass("box01")) {
                console.log("mouseover box01")
            } else if ($(this).hasClass("box02")) {
                console.log("mouseover box02")
            } else if ($(this).hasClass("box03")) {
                console.log("mouseover box03")
            } else if ($(this).hasClass("box04")) {
                console.log("mouseover box04")
            } else {}
        });
    </script>
</body>
</html>
```

### toast弹窗实现
- transition: [transition-property/css属性] [transition-duration/动画时间] [transition-timing-function/动画如何完成一个周期] [transition-delay/动画延时]
- transition 和 animation的区别：
  - transition 是令一个或多个可以用数值表示的css属性值发生变化时产生过渡效果。 animation 则是属于关键帧动画的范畴，它本身被用来替代一些纯粹表现的javascript代码而实现动画
- transform：变形、形变
  - 针对translate、translateX（X轴平移）、translateY（Y轴平移）、rotate（旋转）、scale（缩放）、skew（扭曲）
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
        #toast1,
        #toast2 {
          display: none;
          position: fixed;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          width: 150px;
          border-radius: 10px;
          text-align: center;
          font-size: 12px;
          line-height: 40px;
          color: #fff;
          background: rgba(0, 0, 0, .7);
        }
    </style>
</head>
<body>
    <!-- 实现1 -->
    <button id="toastBtn1">toast btn1</button>
    <div id="toast1"></div>

    <!-- 实现2 -->
    <button id="toastBtn2">toast btn2</button>
    <div id="toast2"></div>

    <!-- 实现3 -->
    <button id="toastBtn3">toast btn3</button>

    <script src="https://code.jquery.com/jquery-1.12.4.min.js" integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=" crossorigin="anonymous"></script>
    <script type="text/javascript">
        $("body")
            .on("click", "#toastBtn1", function() {
                $("#toast1").text("hello, i'm toast1.");
                $("#toast1").fadeIn().delay(1000).fadeOut();
            })
            .on("click", "#toastBtn2", function() {
                $("#toast2").text("hello, i'm toast2.").show();
                setTimeout(() => {
                    $("#toast2").hide();
                }, 1000);
            })
            .on("click", "#toastBtn3", function() {
                ToastFn("hello, i'm toast3.", 1000);
                // 封装成了函数
                function ToastFn(msg, duration) {
                    duration = isNaN(duration) ? 3000 : duration;
                    var toast = document.createElement('div');
                    toast.innerHTML = msg;
                    toast.style.cssText = `
                        position: fixed;
                        top: 50%;
                        left: 50%;
                        transform: translate(-50%, -50%);
                        transition: opacity .5s ease-in-out;
                        width: 150px;
                        border-radius: 10px;
                        text-align: center;
                        font-size: 12px;
                        line-height: 40px;
                        color: #fff;
                        background: rgba(0, 0, 0, .7);
                    `;
                    document.body.appendChild(toast);
                    // 第一个setTimeout：duration后添加渐入渐出样式，同时opacity设为0，toast元素消失
                    setTimeout(function() {
                        toast.style.opacity = '0';
                        /* 第二个setTimeout：虽然上面给 toast元素 设置了opacity为0，元素从页面上消失了
                        但是标签还在html中，多次点击会向body中append多个toast元素，所以第二个setTimeout的目的在于 在宏任务中移除 toast元素：题外话，如果不使用setTimeout直接移除，渐入渐出的样式效果就无法表现出来  */
                        setTimeout(function() {
                            document.body.removeChild(toast);
                        });
                    }, duration);
                }
            });
    </script>
</body>
</html>
```





[viewportFitPic]:data:image/png;base64,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