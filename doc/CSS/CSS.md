### 相邻兄弟选择器(Adjacent sibling selector)
1. 适用场景：二者有相同的父元素，选择紧接在一个元素后的另一个元素
2. e.g. 给紧跟在 h1标签 后出现的 p标签 设置上外边距
``` javascript
    h1 + p {margin-top:50px;}
```