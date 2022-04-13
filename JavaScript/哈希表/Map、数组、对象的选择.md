# Map、数组、对象的选择



## 1.map

```js
//创建对象
let map=new Map();
//存入数据
map.set('age','15'); //两种方法最好不要混用，同一个Map对象最好始终用一个存数据方法
map["a2"]="bbb";
//取数据
map.get('age'); // 取方法和存方法要对应，否则取不出来，set对应get，[]对应[]
console.log(map["a2"]);
//删数据
map.delete('age');
```

- Map
  - 默认`不包含任何键`
  - 提供`has`方法，与`get`复杂度相同，但无需区分`undefined`与假值。语义`可读性`更好
  - 优化了`频繁增删键值对`的场景，在大量数据`增删`时，提升明显



## 2.Array

```javascript
//创建对象
let arr=new Array(); //也可指定长度或参数列表
//存入数据
arr.push(data1); //可存任意类型
arr[index]=data2;
//取数据
console.log(arr[index]);
//删数据（效果见下图）
  //var arr=new Array();
  //arr[0]='apple';
  //arr[1]='banana';
  //console.log(arr);
arr.splice(1,1); //两个参数分别为起始索引和删除个数。使用该方法，数组长度相应改变,但是原来的数组该元素后的元素的索引也相应改变
  //console.log(arr);
delete arr[0]; //这种方式数组长度不变,删除的元素变为undefined,原来数组的索引也保持不变
  //console.log(arr);
```

- 举例：4个数组都是 [ -227 , 227 ]，用`Array`作哈希表
  - `Array`长度为`227 * 2`，(0, 227 * 2)间除了`227`都是`empty`
  - 负数索引，不影响数组长度，会变为`对象属性`，查找和`Object`一样



## 3.Object

```javascript
//创建对象
let obj=new Object();
//存入数据
obj.key = 'apple'; //该方式的方式是指定key的内容，多用于定向赋值
obj[key] = 'apple'; //该方式key是可以动态改变的，可以给对象动态赋值
//取数据
console.log(obj.key); //console.log(geoCoordMap.北京);
concole.log(boj["key"]); //console.log(geoCoordMap["北京"]);
//删数据
delete obj.key;
```

- Object可以解决键名不连续问题，又引入新问题：
  - 查询或for...in遍历对象属性，会读取原型链上的属性
    - 可通过Object.create(null)创建无继承的对象
    - 或用Object.hasOwnproperty(属性名)代替对象.属性名判断属性是否存在



## 4.小节

- 键名多连续，极小值极大值差小，优先数组
- 键名按小到大排序，优先 数组 或 Object
- 键名按插入顺序排序。优先 Map
- 频繁读取`长度`。优先 数组，Map
- 频繁增删键值对。优先 Map



