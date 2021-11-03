## css
### 文字单行超出省略号儿
```css
overflow: hidden; //超出的文本隐藏
text-overflow: ellipsis; //溢出用省略号显示
white-space: nowrap; //溢出不换行
```
### 文字n行超出省略号儿
```css
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box; // 作为弹性伸缩盒子模型显示。
-webkit-box-orient: vertical; // 设置伸缩盒子的子元素排列方式--从上到下垂直排列
-webkit-line-clamp: n; // n为显示的行数
```

### 获取数组中某项的索引，indexOf Polyfill
```javascript
!Array.prototype.indexOf && Array.prototype.indexOf = function(item) {
    for(var i = 0; i < this.length; i++) {
        if(this[i] === item) {
            retrun i;
        }
    }
}
```

### 获取url query参数值
```javascript
function getSearchParams() {
  const { search } = window.location;
  if (!search) return '';
  return search
    .slice(1)
    .split('&')
    .map((group) => group.split('='))
    .reduce((searchParamsObj, item) => {
      searchParamsObj[item[0]] = item[1];
      return searchParamsObj;
    }, {});
}
```



