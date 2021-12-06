## Array
### ECMAScript数组中每个槽位可以存储任意类型的数据(动态数组)
#### 创建数组
```js
//from()用于将类数组结构转换为数组实例
//of()用于将一组参数转换为数组实例

console.log(Array.from("Matt"));//["M","a","t","t"]

const m = new Map().set(1,2)
                   .set(3,4);
const s = new Set().add(1)
.add(2)
.add(3)
.add(4);

console.log(Array.from(m));//[[1,2],[3,4]]
console.log(Array.from(s));//[1,2,3,4]

//Array.from()对现有数组执行浅复制
const a1 = [1,2,3,4];
const a2 = Array.from(a1);

console.log(a1); // [1,2,3,4]
alert(a1===a2);//false

//可以使用 任何可迭代对象
const iter ={
    *[Symbol.iterator](){
        yield 1;
        yield 2;
        yield 3;
        yield 4;
    }
};

console.log(Array.from(iter));//[1,2,3,4]

from()可接收第一个可选的映射函数参数
const a1 = [1,2,3,4];
const a2 = Array.from(a1,x => x**2);

console.log(a2);//[1,4,9,16]

```
#### 数组空位
使用数组字面量初始化数组时，可以使用一窜逗号来创建空位(hole)
```js
const options = [,,,,,];//创建包含5个元素的数组
console.log(options.length);//5

const options = [1, , , , 5];
    for (const option of options) {
            console.log(option);
        }
     for (const [index, value] of options.entries()) {
            console.log(value);
        }
        //1 undefined undefined undeined 5
    
    const a = Array.from([,,,]);//使用ES6的Array.from()创建的包含3个空位的数组
    for(const val of a){
        alert(val === undefined);
    }// true true true

```
#### 检测数组
```js
if(value instanceof Array){
    //操作数组
}

if（Array.isArray(value)){
    //操作数组 
}
```
#### 迭代器方法
```js
const a = ["foo","bar","baz","qux"];

const aKeys = Array.from(a.keys());
const aValues = Array.from(a.values());
const aEntries = Array.from(a.entries());

console.log(aEntries);//{[0,"foo"],[1,"bar"],[2,"baz"].[3,"qux"]};
```

#### 队列方法
```js
let colors = new Array();
let count = colors.push("red","green");
alert(count);//2

count = colors.push("black");
alert(count);//3

let item = colors.shift();//取得第一项
alert(item);//red
alert(colors.length);//2

反向队列:

let colors = new Array();
let count = colors.unshift("black","red","green");

let item = colors.pop();//取得最后一项
alert(item); // green
alert(colors.length);//2
```
#### 排序方法

```js
function compare(value1, value2){
    if(value1<value2){
        return -1;
    }else if(value1 > value2){
        return 1;
    }else{
        return 0;
    }
}

let values = [0,1,5,10,15];
values.sort(compare);
alert(values);//0,1,5,10,15

箭头函数
values.sort((a,b) => a<b ? 1:a>b ? -1 :0);

```

#### 操作方法
```js
let colors = ["red","green","blue"];
let newColors = ["black","brown"];
let moreNewColors = {
    [Symbol.isConcatSpreadable]: true,
    length:2,
    0:"pink",
    1:"cyan"
};

newColors[Symbol.isConcatSpreadable] = false;

//强制不打平数组
let colors2 = colors.concat("yallow",newColors);

//强制打平数组对象
let colors3 = colors.concat(moreNewColors);

console.log(colors); //["red","green","blue"]
console.log(colors2);//["red","green","yellow",["black","brown"]];
coonsole.log(colors3)//["red","green","blue","pink","cyan"];

```
##### splice
```js
let colors = ["red", "green", "blue"]; 
let removed = colors.splice(0,1); // 删除第一项
alert(colors); // green,blue 
alert(removed); // red，只有一个元素的数组
removed = colors.splice(1, 0, "yellow", "orange"); // 在位置 1 插入两个元素
alert(colors); // green,yellow,orange,blue 
alert(removed); // 空数组
removed = colors.splice(1, 1, "red", "purple"); // 插入两个值，删除一个元素
alert(colors); // green,red,purple,orange,blue 
alert(removed); // yellow，只有一个元素的数
```
##### 搜索和位置方法
1、严格相等
```js
let numbers = [1,2,3,4,5,4,3,2,1];

alert(numbers.indexOf(4)); //3
alert(numbers.lastIndexOf(4)); //5
alert(numbers.includes(4));//true

alert(numbers.indexOf(4,4)); //5
```
2、断言函数
```js
const people = {
    {
        name:"Matt",
        age:27
    },
    {
        name:"Nicholas",
        age:29
    }
};

alert(people.find((element,index,array) => element.age < 28));
//{name:"Matt",age:27}
alert(people.find((element,index,array) => element.age < 28));
//0

//找到匹配项后，这两个方法都不能再继续搜索
const evens = {2,4,6};

evens.find((elements,index,array) => {
    console.log(element);
    console.log(index);
    console.log(array);
    return element === 4;
})
//2 0 [2,4,6] 4 1 [2,4,6]
```
##### 迭代方法
every()：对数组每一项都运行传入的函数，如果对每一项函数都返回 true，则这个方法返回 true。
filter()：对数组每一项都运行传入的函数，函数返回 true 的项会组成数组之后返回。
forEach()：对数组每一项都运行传入的函数，没有返回值。
map()：对数组每一项都运行传入的函数，返回由每次函数调用的结果构成的数组。
some()：对数组每一项都运行传入的函数，如果有一项函数返回 true，则这个方法返回 true。
这些方法都不改变调用它们的数组。
```js
let numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];

let everyResult = numbers.every((item,index,array) => item > 2);
alert(everyResult); //false

let someResult = numbers.some((item,index,array) => item >2 );
alert(someResult);//true

let filterResult = numbers.filter((item,index,array() => item > 2));
alert(filterResult);//3,4,5,4,3

let mapResult = numbers.map((item,index,array) => item * 2);
alert(mapResult);//2.4.6.8.10.8.6.4.2
```
##### 归并方法

```js
let values = {1,2,3,4,5}
let sum = values.reduce((prev,cur,index,array) => prev + cur);

alert(sum);//15

let sum = values.reduceRight(function(prev,cur,index,array){
    return prev + cur;
});

alert(sum);//15

//reduce（）与reduceRight（）的区别知识遍历数组元素的方向不同。
```

#### 定型数组

##### ArrayBuffer
```js
const buf = new ArrayBuffer(16)//在内存中分配16字节
alert(buf.byteLength);//16
//ArrayBuffer一经创建就不能再调整大小，但能复制
const buf1 = new ArrayBuffer(16);
const buf2 = buf1.slice(4,12);
alert(buf2.byteLength);//8
```
##### DataView
```js
const buf = new ArrayBuffer(16);

const fullDataView = new DataView(buf);//(buf,0,8);
alert(fullDataView.byteOffset);//0
alert(fullDataView.byteLength);//16
alert(fullDataView.buffer === buf);//true

1.ElementType
const buf = new ArrayBuffer(2);
const view = new DataView(buf);

//说明整个缓冲确实所有二进制位都是0
//检查第一个和第二个字母
alert(view.getInt8(0));//0
alert(view.getInt8(1));//0
//检查整个缓冲
alert(view.getInt16(0));//0

//将整个缓冲都设置为1
//255的二进制表示是1111 1111（2^8-1）
view.setUint8(0,255);

//DataView 会自动将数据转换为特定的ElementType
//255的十六进制表示是OxFF
view.setUint8(1,OxFF);

//现在，缓冲里都是1了
//如果把它当成二补数的有符号整数，则应该是-1
alert(view.getInt16(0)); //-1ui1ywe
```

2.字节序
```js
//字节序指的是计算系统维护的一种字节顺序的约定。

//在内存中分配两个字节并声明一个DataView
const buf = new ArrayBuffer(2);
const view = new DataView(buf);

//填充缓冲，让第一位和最后一位都是1
view.setUint8(0,0x80);//设置最左边的位等于1
view.setUint8(1,0x01);//设置最右边的位等于1

//缓冲内容（为方便阅读，人为加了空格）
//0x8 0x0 0x0 0x1
//1000 0000 0000 0001

//按大端字节序读取Uint16
// 0x01 是高字节，0x80 是低字节
// 0x0180 = 2^8 + 2^7 = 256 + 128 = 384 
alert(view.getUint16(0, true)); // 384

// 按大端字节序写入 Uint16 
view.setUint16(0, 0x0004);

// 缓冲内容（为方便阅读，人为加了空格）
// 0x0 0x0 0x0 0x4 
// 0000 0000 0000 0100 

alert(view.getUint8(0)); // 0 
alert(view.getUint8(1)); // 4

// 按小端字节序写入 Uint16 
view.setUint16(0, 0x0002, true);

// 缓冲内容（为方便阅读，人为加了空格）
// 0x0 0x2 0x0 0x0 
// 0000 0010 0000 0000

alert(view.getUint8(0)); // 2 
alert(view.getUint8(1)); // 0 
```
#### 定型数组
```js
//定型数组的目的就是提高与 WebGL 等原生库交换二进制数据的效率
// 创建一个 12 字节的缓冲
const buf = new ArrayBuffer(12); 
// 创建一个引用该缓冲的 Int32Array 
const ints = new Int32Array(buf); 
// 这个定型数组知道自己的每个元素需要 4 字节
// 因此长度为 3 
alert(ints.length); // 3

//如果定型数组没有用任何值初始化，则其关联的缓冲会以 0 填充：
const ints = new Int32Array(4); 
alert(ints[0]); // 0 
alert(ints[1]); // 0 
alert(ints[2]); // 0 
alert(ints[3]); // 0 
```
1.合并、复制和修改定型数组
```js
// 创建长度为 8 的 int16 数组
const container = new Int16Array(8); 
// 把定型数组复制为前 4 个值
// 偏移量默认为索引 0 
container.set(Int8Array.of(1, 2, 3, 4)); 
console.log(container); // [1,2,3,4,0,0,0,0] 
// 把普通数组复制为后 4 个值
// 偏移量 4 表示从索引 4 开始插入
container.set([5,6,7,8], 4); 
console.log(container); // [1,2,3,4,5,6,7,8] 

const source = Int16Array.of(2, 4, 6, 8); 
// 把整个数组复制为一个同类型的新数组
const fullCopy = source.subarray(); 
console.log(fullCopy); // [2, 4, 6, 8] 
// 从索引 2 开始复制数组
const halfCopy = source.subarray(2); 
console.log(halfCopy); // [6, 8] 
// 从索引 1 开始复制到索引 3 
const partialCopy = source.subarray(1, 3); 
console.log(partialCopy); // [4, 6] 
```
#### WeakMap

##### 基本API
```js
const wm = new WeakMap();
const key1 = {id:1},
      key2 = {id:2},
      key3 = {id:3};
//使用嵌套数组初始化弱映射
const wm1 = new WeakMap([
    [key1,"val1"],
    [key1,"val2"],
    [key3,"val3"]
]);
alert(wml.get(key1));//val1
alert(wml.get(key2));//val2
alert(wml.get(key3));//val3

//初始化是全有或全无的操作
//只要有一个键无效就会抛出错误，导致整个初始化失败
const wm2 = new WeakMap([
    [key1,"val1"],
    ["BADKEY","val2"],
    [key3,"val3"]
]);
//TypeError:Invalid value used as WeakMap key typeof wm2;
//ReferenceError:wm2 is not defined

//原始值可以先包装成对象再用作键
const stringKey = new String("key1");
const wm3 = new WeakMap([
    stringKey,"vall"
]);
alert(wm3.get(stringKey));//"vall"
```
##### 弱键
```js
const wm = new WeakMap();

wm.set({},"val");
//因为没有指向这个对象其他引用，在这行代码执行完毕后就会成为垃圾回收的目标
const wm = new WeakMap();

const container = {
    key:{}
};

wm.set(container.key,"val");

function removeReferenece(){
    container.key= null;
}
//container对象维护着一个弱映射键的引用，因此这个对象不会成为垃圾回收的目标。
```
##### 使用弱映射

