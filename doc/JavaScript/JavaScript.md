JavaScript.md

### 数组方法
|方法名 |作用              |返回值    |是否修改原数组|备注|
|:----:|:---------------|:-------:|:----------:|:--|
|push|数组后增|数组length|是|
|unshift|数组前增|数组length|是|
|pop|数组后删|被删除的项|是|
|shift|数组前删|被删除的项|是|
|indexOf|寻找数组中某项对应的下标|Number(-1表示不包含目标项)|否|一般针对简单数据类型|
|findIndex|寻找数组中某项对应的下标|Number(-1表示不包含目标项)|否|一般针对引用类型|回调函数入参：(callback(Value[, Index[, Array]])[, thisArg])；thisArg 执行 callback 时用于 this 的值|
|find|寻找数组中第一个满足某条件的项|目标项 or undefined|否|同findIndex|
|fitler|过滤数组中所有满足某条件的项|Array|否|同findIndex|
|includes|判断数组中是否包含某项|Boolearn|否|
|some|判断数组中是否包含满足某条件的项|Boolearn|否|同findIndex|
|every|判断数组中是否所有项都满足某条件|Boolearn|否|同findIndex|
|map|根据需求格式化数组|Array|否|同findIndex|
|forEach|单纯迭代|无|否|同findIndex|
|concat|数组合并|Array|否|
|slice|数组截取|Array（由被截取项组成）|否|入参：([beginIndex[, endIndex]])|
|splice|数组截取并插入新项|Array（由被删除项组成）|是|(startIndex[, deleteCount[, item1[, item2[, ...]]]])；deleteCount为0时，新项就从start位置开始插入|
|reduce|数组累加器|可以是任意类型|否|[使用说明](https://chinese.freecodecamp.org/news/the-ultimate-guide-to-javascript-array-methods-reduce/)|

- 几点说明
  - 入参为回调函数的几个方法，回调函数的入参相同
    - indexOf、findIndex、find、fitler、some、every、map、forEach：回调函数入参：(callback(Value[, Index[, Array]])[, thisArg])；thisArg 执行 callback 时用于 this 的值
  - 针对 slice方法 的几点说明
    - 该方法也可用于 String类型，返回值为 被截取项组成的String
    - 如果省略 beginIndex，则 slice 从索引 0 开始 --> 数组的浅拷贝
    - **截取部分不包含 endIndex**
    - 省略endIndex会截取到末尾；负数表示从末尾开始截取：-1表示最后一项，-2表示倒数第二项
  - 封装insert方法
```javascript
    Array.prototype.insert = function(index, item) {
        this.splice(index, 0, item);
    }
```
