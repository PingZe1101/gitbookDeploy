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

## 新东方大学事业部国庆、双11抽奖活动
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







