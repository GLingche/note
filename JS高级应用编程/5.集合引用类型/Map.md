### Map
#### 基本API
```js

const m1 = new Map([
    ["key1","val1"],
    ["key2","val2"],
    ["key3","val3"]  
]);
alert(m1.size);//3

//映射期待的键/值对，无论是否提供
const m3 = new Map([[]]);
alert(m3.has(undefined));//true
alert(m3.get(undefined));//undefined

const m = new Map();

alert(m.has("firstName"))//false
alert(m.get("firstName"))//undefined

m.set("firstNAME","Matt")
 .set("lastNmae","Frisbie");

m.delete("firstName");//只删除这一个键/值对

m.clear();

Map可以使用任何数据类型作为键
const m = new Map();

const functionKey = function(){};
const symbolKey = Symbol();
const objedtKey = new Object();

m.set(functionKey,"functionValue");
m.set(symbolKey,"symbolValue");
m.set(objectKey,"objectValue");

alert(m.get(functionKey));//functionValue

//SameValueZero 比较意味着独立实例不冲突
alert(m.get(function(){}));//undefined  

```
#### 顺序与迭代
```js
const m = new Map([
    ["key1","val1"],
    ["key2","val2"],
    ["key3","val3"]
]);

alert(m.entries === m[Symbol.iterator]);//true

for(let pair of m.entries()){
    alert(pair);
}
//[key1,val1]
//[key2,val2]
//[key3,val3]

for(let pair of m[Symbol.iterator]()){
    alert(pair);
}
//[key1,val1]
//[key2,val2]
//[key3,val3]

//forEach 回调
m.forEach(val,key) => alert(`${key} -> ${val}`));
//key1 -> val1
//key2 -> val2
//key3 -> val3
```
#### 选择Object还是Map
对于多数 Web 开发任务来说，选择 Object 还是 Map 只是个人偏好问题，影响不大。不过，对于
在乎内存和性能的开发者来说，对象和映射之间确实存在显著的差别。
##### 内存占用
Object 和 Map 的工程级实现在不同浏览器间存在明显差异，但存储单个键/值对所占用的内存数量
都会随键的数量线性增加。批量添加或删除键/值对则取决于各浏览器对该类型内存分配的工程实现。
不同浏览器的情况不同，但给定固定大小的内存，Map 大约可以比 Object 多存储 50%的键/值对。
##### 插入性能
向 Object 和 Map 中插入新键/值对的消耗大致相当，不过插入 Map 在所有浏览器中一般会稍微快
一点儿。对这两个类型来说，插入速度并不会随着键/值对数量而线性增加。如果代码涉及大量插入操
作，那么显然 Map 的性能更佳。
##### 查找速度
与插入不同，从大型 Object 和 Map 中查找键/值对的性能差异极小，但如果只包含少量键/值对，
则 Object 有时候速度更快。在把 Object 当成数组使用的情况下（比如使用连续整数作为属性），浏
览器引擎可以进行优化，在内存中使用更高效的布局。这对 Map 来说是不可能的。对这两个类型而言，
查找速度不会随着键/值对数量增加而线性增加。如果代码涉及大量查找操作，那么某些情况下可能选
择 Object 更好一些。
##### 删除性能
使用 delete 删除 Object 属性的性能一直以来饱受诟病，目前在很多浏览器中仍然如此。为此，
出现了一些伪删除对象属性的操作，包括把属性值设置为 undefined 或 null。但很多时候，这都是一
种讨厌的或不适宜的折中。而对大多数浏览器引擎来说，Map 的 delete()操作都比插入和查找更快。
如果代码涉及大量删除操作，那么毫无疑问应该选择 Map    