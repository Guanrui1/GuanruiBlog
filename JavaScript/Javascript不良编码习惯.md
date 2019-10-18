### 黎叔很生气，后果很严重

<img src="../images/angry.jpg">

不知道从可是起，再次回看自己之前写的代码，会有种砸键盘的冲动😠

* 你几乎看不懂之前的代码时什么意思
* 之前使用了比较骚的操作，导致后继无人😓
* 给孩子起名字太随意，甚至还没有张三李四王五叫着清晰和顺口。

其实这些问题都是由于自己平时不注意养成良好的编码习惯导致的，所谓天道酬勤，光是懒时没有前途的，哪怕你是为了节省时间相处的巧妙的方法，也不是懒的借口，总之一句话，懒就玩完了😁

> 下面我们就来总结几条我们平时经常会犯的错误

### 1、不要使用隐式类型转换
JavaScript是一种松散类型的语言。 如果使用得当，这是一个好处，因为它给你带来了灵活性。
大多数运算符+ - * / ==(不包括 ===)在处理不同类型的操作数时会进行隐式转换。
语句if（condition）{...}，while（condition）{...}隐式地将条件转换为布尔值。
下面的示例依赖于类型的隐式转换，这种有时候会让人感到很困惑：
```javascript
console.log("2" + "1");  // => "21"
console.log("2" - "1");  // => 1

console.log('' == 0);    // => true

console.log(true == []); // -> false
console.log(true == ![]); // -> false
```

过度依赖隐式类型转换是一个坏习惯。 首先，它使你的代码在边缘情况下不太稳定。 其次，增加了引入难以重现和修复的bug的机会。
现在咱们实现一个获取对象属性的函数。如果属性不存在，函数返回一个默认值
```javascript
function getProp(object, propertyName, defaultValue) {
  if(!object[propertyName]) {
    return defaultValue
  }
  return object[propertyName]
}

const hero = {
  name: 'Spider',
  address: 'New York',
  isChild: false
}

console.log(getProp(hero, 'address', 'Unknown')) // => 'New York'
```
上述代码确确实实的能够获取到hero的address属性的值，然后显示出来但是，假如我们去获取isChild的值，那么我们的代码就会出问题，你会返现
```javascript
console.log(getProp(hero, 'isChild', true)) // => true
```
也就是说，即使你的实际值是false，用咱么的整个提取函数去取值那么依然会取到false，也就是说我们造的整个看似合理的轮子，其实隐藏了一个这种很隐蔽的bug，这是因为属性存在的验证依赖于if（！object [propertyName]）{...}隐式转换的布尔值。
这些错误很难发现，要修复该函数，就要明确验证值的类型：
```javascript
function getPropFixed(object, propertyName, defaultValue) {
  if(object[propertyName] === undefined) {
    return defaultValue
  }
  return object[propertyName]
}

const hero = {
  name: 'Spider',
  address: 'New York',
  isChild: false
}

console.log(getPropFixed(hero, 'isChild', true)) // => false
```
`object[propertyName] === undefined`确切地验证属性是否为`undefined`。
这里建议避免直接使用`undefined`。 因此，上述解决方案可以进一步改进：
```javascript
function getPropFixedBetter(object, propertyName, defaultValue) {
  if(!(propertyName in object)) {
    return defaultValue
  }
  return object[propertyName]
}
```
尽可能不要使用隐式类型转换。相反，请确保变量和函数参数始终具有相同的类型，必要时使用显式类型转换。
##### 最佳实践列表：
* 始终使用严格的相等运算符===进行比较
* 不要使用松散等式运算符==
* 加法运算符 operand1 + operand2：两个操作数应该是数字或字符串
* 算术运算符 - * /％**：两个操作数都应该是数字
* if（condition）{...}，while（condition）{...}等语句：condition 必须是一个布尔类型值

写到这里，突然想到，就是我们在实际的vue项目中，很多时候需要使用v-if来控制元素的显示与隐藏，而规定一般都是如果后台传了数据，且数据不为空的话，就使其为true，否则就为false，这里其实我们可以用computed来实现，用computed的好处自然时缩短代码，做到见名知义。尽量使自己代码中不存在或者很少存在大跨度的令人莫不着头脑的代码，用了computed之后，我们还可以使用&&来一次获取对象的属性值，这样的好处就是可以避免代码报错，比如以下这种情况:
```javascript
let a = undefined
console.log(a.length)
```
如果直接获取一个undefined的length属性，那么就会报错，假如我们这样写
```javascript
let a = undefined
let temp = a && a.length
console.log(temp)
```
用computed的话也是这个原理，这样就可以避免获取位置代码的错误，因为这种短路运算符，在第一个参数为undefined或不存在时就不会往后执行了