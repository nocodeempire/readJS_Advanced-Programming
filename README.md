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
switch 语句中使用任何数据类型（在很多其他语言中只能使用数值），无论是字符串，还是对象都没有问题。  
其次，每个 case 的值不一定是常量，可以是变量，甚至是表达式。
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
typeof检测基本数据类型,很适用;但引用类型就不行了,typeof null === "object" 为true.   
instanceof运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。  
所有引用类型的值都是 Object 的实例。因此，在检测一个引用类型值和 Object 构造  
函数时， instanceof 操作符始终会返回 true。当然，如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false，因为基本类型不是对象。
#### 垃圾回收
1.标记清除 现代浏览器应该都是标记清除,这种算法的思想是给当前不使用的值加上标记，然后再回收其内存。  
2.引用计数 存在相互引用导致内存一直占用可能
#### Array
push() 方法可向数组的末尾添加一个或多个元素,并返回新的长度  
pop() 方法用于删除并返回数组的最后一个元素  
unshift() 方法可向数组的开头添加一个或更多元素,并返回新的长度  
shift() 方法用于把数组的第一个元素从其中删除,并返回第一个元素的值  
indexOf()和 lastIndexOf()方法查找特定项在数组中的位置(可以是对象在数组中的位置),存在返回索引,不存在-1
 every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true。  
 filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。  
 forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。  
 map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。  
 some()：对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true。  
以上方法都不会修改数组中的包含的值  
还有两个归并数组的方法： reduce()和 reduceRight(), 但个人觉得应用场景不多. 能实现数组求和,去重等,但都有更好的方法.
#### Date
Date.parse()方法接收一个表示日期的字符串参数，然后尝试根据这个字符串返回相应日期的毫秒数。(不推荐在ES5之前使用Date.parse方法，因为字符串的解析完全取决于实现。直到至今，不同宿主在如何解析日期字符串上仍存在许多差异，因此最好还是手动解析日期字符串)  
Data.now()方法，返回表示调用这个方法时的日期和时间的毫秒数.  
注意: Date对象的各种XXXString()方法在不同浏览器上显示都是不同的,不具有实际用途,所有真正实际项目中格式化日期还是需要自己获取时分秒年月日等
#### RegExp(薄弱项)
 g：表示全局（global）模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止  
 i：表示不区分大小写（case-insensitive）模式，即在确定匹配项时忽略模式与字符串的大小写  
 m：表示多行（multiline）模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。  
````js
// 匹配第一个"bat"或"cat"，不区分大小写
var pattern1 = /[bc]at/i;
// 与 pattern1 相同，只不过是使用构造函数创建的
var pattern2 = new RegExp("[bc]at", "i");
````
看到5.5.1 明天继续











