# JavaScriptFragment
超实用的JavaScript代码片段

# Array数组
### Array concatention(数组拼接)
使用Array.cancat,通过args中附加任何数组或值来拼接一个数组
```
const ArrayConcat = (arr,...args) =>{
  [].concat(arr,...args)
}
```
### Array difference(数组比较)
根据数组b创建一个Set对象，然后在数组a上使用Array.filter()方法过滤出数组b中不包含的值,has() 方法返回一个布尔值来指示对应的值value是否存在Set对象中
```
const difference = (a,b) => {
  const s = new Set(b)
  return a.filter(x => !s.has(x))
}
```
### Array includes(数组包含)
使用slice()来抵消数组/字符串，并且使用indexOf()来检查是否包含该值。如果省略最后一个参数fromIndex,则会检查整个数组/字符串。
```
const includes = (collection, val,fromIndex=0) => {
  return collection.slice(fromIndex).indexOf(val) != -1
}
```
### Array remove (移除数组中的元素)
使用 Array.filter() 和 Array.reduce() 来查找返回真值的数组元素，使用 Array.splice() 来移除元素。 func 有三个参数(value, index, array)。
```
const remove = (arr, func) =>
  Array.isArray(arr) ? arr.filter(func): [];
//remove([1, 2, 3, 4], n => n % 2 == 0) -> [2, 4]
```
### Array sample (数组取样随，机获取数组中的1个元素)
使用 Math.random() 生成一个随机数，乘以 length，并使用 Math.floor() 舍去小数获得到最接近的整数。这个方法也适用于字符串。
```
const sample = arr => arr[Math.floor(Math.random() * arr.length)];
// sample([3, 7, 9, 11]) -> 9
```
### Array union (数组合集)
用数组 a 和 b 的所有值创建一个 Set 对象，并转换成一个数组
```
const union = (a, b) => Array.from(new Set([...a, ...b]));
// union([1,2,3], [4,3,2]) -> [1,2,3,4]
```
### Array without (从数组中排除给定值)
使用 Array.filter() 创建一个排除所有给定值的数组。
```
const without = (arr, ...args) => arr.filter(v => args.indexOf(v) === -1);
// without([2, 1, 2, 3], 1, 2) -> [3]
// without([2, 1, 2, 3, 4, 5, 5, 5, 3, 2, 7, 7], 3, 1, 5, 2) -> [ 4, 7, 7 ]
```
### Array zip (创建一个分组元素数组)
使用 Math.max.apply() 获取参数中最长的数组。 创建一个长度为返回值的数组，并使用 Array.from() 和 map-function 来创建一个分组元素数组。 如果参数数组的长度不同，则在未找到值的情况下使用 undefined 。
```
const zip = (...arrays) => {
  const maxLength = Math.max.apply(null, arrays.map(a => a.length));
  return Array.from({length: maxLength}).map((_, i) => {
   return Array.from({length: arrays.length}, (_, k) => arrays[k][i]);
  })
}
//zip(['a', 'b'], [1, 2], [true, false]); -> [['a', 1, true], ['b', 2, false]]
//zip(['a'], [1, 2], [true, false]); -> [['a', 1, true], [undefined, 2, false]]
```
### Average of array of numbers (求数字数组的平均数)
使用 Array.reduce() 将数组中的每个值添加到一个累加器，使用 0 初始化，除以数组的 length (长度)。
```
const average = arr => arr.reduce((acc, val) => acc + val, 0) / arr.length;
// average([1,2,3]) -> 2
```
### Chunk array (数组分块)
使用 Array.from() 创建一个新的数组，它的长度与将要生成的 chunk(块) 数量相匹配。 使用 Array.slice() 将新数组的每个元素映射到长度为 size 的 chunk 中。 如果原始数组不能均匀分割，最后的 chunk 将包含剩余的元素。Math.ceil()向上取整。
```
const chunk = (arr, size) =>
  Array.from({length: Math.ceil(arr.length / size)}, (v, i) => arr.slice(i * size, i * size + size));
// chunk([1,2,3,4,5], 2) -> [[1,2],[3,4],[5]]
```
### Compact (过滤掉数组中所有假值元素)
使用 Array.filter() 过滤掉数组中所有 假值元素(false, null, 0, "", undefined, and NaN)。
```
const compact = (arr) => arr.filter(v => v);
// compact([0, 1, false, 2, '', 3, 'a', 'e'*23, NaN, 's', 34]) -> [ 1, 2, 3, 'a', 's', 34 ]
```
### Count occurrences of a value in array (计数数组中某个值的出现次数)
每次遇到数组中的指定值时，使用 Array.reduce() 来递增计数器。
```
const countOccurrences = (arr, value) => arr.reduce((a, v) => v === value ? a + 1 : a + 0, 0);
// countOccurrences([1,1,2,1,2,3], 1) -> 3
```
### Deep flatten array (深度平铺数组)
使用递归。 通过空数组([]) 使用 Array.concat() ，结合 展开运算符( ... ) 来平铺数组。 递归平铺每个数组元素。
```
const deepFlatten = arr => [].concat(...arr.map(v => Array.isArray(v) ? deepFlatten(v) : v));
// deepFlatten([1,[2],[[3],4],5]) -> [1,2,3,4,5]
```
### Filter out non-unique values in an array (过滤出数组中的非唯一值)
```
const filterNonUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i));
// filterNonUnique([1,2,2,3,4,4,5]) -> [1,3,5]
```
### Flatten array up to depth (根据指定的 depth 平铺数组)
每次递归，使 depth 减 1 。使用 Array.reduce() 和 Array.concat() 来合并元素或数组。默认情况下， depth 等于 1 时停递归。省略第二个参数 depth ，只能平铺1层的深度 (单层平铺)。
```
const flattenDepth = (arr, depth = 1) =>
  depth != 1 ? arr.reduce((a, v) => a.concat(Array.isArray(v) ? flattenDepth(v, depth - 1) : v), [])
  : arr.reduce((a, v) => a.concat(v), []);
// flattenDepth([1,[2],[[[3],4],5]], 2) -> [1,2,[3],4,5]
```
### Nth element of array (获取数组的第N个元素)
使用 Array.slice() 获取数组的第 n 个元素。如果索引超出范围，则返回 [] 。省略第二个参数 n ，将得到数组的第一个元素。
```
const nth = (arr, n=0) => (n>0? arr.slice(n,n+1) : arr.slice(n))[0];
// nth(['a','b','c'],1) -> 'b'
// nth(['a','b','b']-2) -> 'a'
```
### Similarity between arrays (获取数组交集)
```
const similarity = (arr, values) => arr.filter(v => values.includes(v));
// similarity([1,2,3], [1,2,4]) -> [1,2]
```
