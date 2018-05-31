# 读javascript高级程序设计笔记
刚开始做前端的时候翻过这本红皮书和犀牛书,差不多都看了一半多,没能坚持看完.现在工作相对清闲.准备看完这两本书.对一些知识点也记录下.

#### typeof
判断类型加不加括号都可以是因为:typeof是一个操作符而不是函数，因此例子中的圆括号尽管可以使用，但不是必需的。
typeof null会返回"object"，因为特殊值 null 被认为是一个空的对象引用
#### NaN
NaN 与任何值都不相等，包括 NaN 本身。
#### 逻辑非
````html
逻辑非操作符由一个叹号（！）表示;
 如果操作数是一个对象，返回 false；  // 注意空对象 以前一直以为!{}是true 其实是false;可以理解成对象总是指向一个地址,例如0x11, 所以!0x11是false
 如果操作数是一个空字符串，返回 true；
 如果操作数是一个非空字符串，返回 false；
 如果操作数是数值 0，返回 true；
 如果操作数是任意非 0 数值（包括 Infinity），返回 false；
 如果操作数是 null，返回 true；
 如果操作数是 NaN，返回 true；
 如果操作数是 undefined，返回 true。
````
#### for in
如果表示要迭代的对象的变量值为 null 或 undefined， for-in 语句会抛出错误。
ECMAScript 5 更正了这一行为；对这种情况不再抛出错误，而只是不执行循环体。
#### switch case
switch 语句中使用任何数据类型（在很多其他语言中只能使用数值），无论是字符串，还是对象都没有
问题。其次，每个 case 的值不一定是常量，可以是变量，甚至是表达式。
````js
switch ("hello world") {
  case "hello" + " world":
    alert("Greeting was found.");
    break;
  default:
    alert("Unexpected message was found.");
}
var num = 25;
switch (true) {
  case num < 0:
    alert("Less than 0.");
    break;
  case num >= 0 && num <= 10:
    alert("Between 0 and 10.");
    break;
  case num > 10 && num <= 20:
    alert("Between 10 and 20.");
    break;
  default:
    alert("More than 20.");
}
````
注意: switch 语句在比较值时使用的是<strong>全等操作符</strong>，因此不会发生类型转换（例如，字符串"10"不等于数值 10）。
#### instanceof与typeof
````html
typeof检测基本数据类型,很适用;但引用类型就不行了,typeof null === "object" 为true. 
instanceof运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。
所有引用类型的值都是 Object 的实例。因此，在检测一个引用类型值和 Object 构造
函数时， instanceof 操作符始终会返回 true。当然，如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false，因为基本类型不是对象。

````



















