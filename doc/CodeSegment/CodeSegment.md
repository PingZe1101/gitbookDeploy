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

### 获取url query参数值
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

### 扩展运算符
#### 合并对象
##### 合并对象1
```javascript
const obj1 = {
  name: 'xiaohei',
  age: 12,
  eat: 'fruit',
}
const obj2 = {
  ...obj1,
  color: 'black',
}
const {eat, ...targetObj} = obj2; // 注意前面的const
console.log(targetObj);
/* {
  name: 'xiaohei',
  age: 12,
  color: 'black',
} */
```
##### 合并对象1
```javascript
  // bad
  function concatenateAll() {
    const args = Array.prototype.slice.call(arguments);
    return args.join('');
  }
  // good
  function concatenateAll(...args) {
    return args.join('');
  }
```
#### 将类数组转换为数组
```javascript
function fn(){return arguments};
const arrayLike = fn('a', 'b', 'c', 'd');
console.log(Object.prototype.toString.call(arrayLike)); // [object Arguments]
const arr1 = Array.prototype.slice.call(arrayLike);
console.log(Object.prototype.toString.call(arr1)); // [object Array]
const arr2 = [...arrayLike];
console.log(Object.prototype.toString.call(arr2)); // [object Array]
```

### 解构 Destructuring
#### 对象解构
```javascript
 // bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
  return `${firstName} ${lastName}`;
}
// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}
// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```
#### 数组解构
```javascript
const arr = [1, 2, 3, 4];
// bad
const first = arr[0];
const second = arr[1];
// good
const [first, second] = arr;
```


