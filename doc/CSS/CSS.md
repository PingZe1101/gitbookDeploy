### 相邻兄弟选择器(Adjacent sibling selector)
1. 适用场景：二者有相同的父元素，选择紧接在一个元素后的另一个元素
2. e.g. 给紧跟在 h1标签 后出现的 p标签 设置上外边距
``` javascript
    h1 + p {margin-top:50px;}
```

### background复合属性写法
- background: background-color background-image background-repeat background-attachment background-position/background-size;
  - background-attachment
    - scroll：背景图片随着页面的滚动而滚动（默认值）
    - fixed：背景图片不会随着页面的滚动而滚动
  - background-position
    - top center bottom left right，如果仅规定了一个关键词 第二个值将是“center”
      - **top left 和 left top 是一样的，都能够识别（已写demo验证）**
  - background-size
    - cover：等比缩放背景图 以完全覆盖掉 背景区域
    - contain：在背景区域内完整地、最大化地展示 背景图（宽高等比缩放）
    - percentage：将计算相对于背景定位区域的百分比。第一个值设置宽度，第二个值设置的高度。如果只给出一个值，第二个是设置为"auto(自动)"
      - 背景区域非正方形的情况下：
        - width > height: contain === 100% auto
        - height > width: contain === auto 100%



