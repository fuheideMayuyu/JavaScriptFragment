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
