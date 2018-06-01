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
#### sort排序
````js
function createComparisonFunction(propertyName) { // sort根据特性属性值排序
  return function(object1, object2){
    var value1 = object1[propertyName];
    var value2 = object2[propertyName];
    if (value1 < value2){
      return -1;
    } else if (value1 > value2){
      return 1;
    } else {
      return 0;
    }
  };
}
var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
data.sort(createComparisonFunction("age"));
alert(data[0].name); //Zachary
````
#### apply call bind
apply与call相对熟悉,平时有用,bind很少用到,语法如下:
````js
window.color = "red";
var o = { color: "blue" };
function sayColor(){
  alert(this.color);
}
var objectSayColor = sayColor.bind(o); // 方法调用的时候把this绑定到o 其实个人觉得bind和call与apply差不多,就是不需要传参
objectSayColor(); //blue
````
#### 基本包装类型
引用类型与基本包装类型的主要区别就是对象的生存期。  
使用 new 操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。  
所以说定义了一个字符串var str = "a", str += "b", 其实是丢弃了a的空间重新在内存中开辟了一个新的空间ab.不过现在浏览器貌似对字符串拼接有改良,性能还不错.
有一点需要注意.有没有关键字new是有区别的
````js
var value = "25";
var number = Number(value); //转型函数
alert(typeof number); //"number"
var obj = new Number(value); //构造函数
alert(typeof obj); //"object"
````
基本类型的数字,例如10,理论上不是对象,应该是不能.方法的,不过js内部应该是做过处理了.所以:  
````js
var num = 10.005;
alert(num.toFixed(2)); //"10.01" toFixed()能够自动舍入
````
string的一些方法
````js
var stringValue = "hello";
alert(stringValue.charAt(1)); //"e" 返回字符
alert(stringValue.charCodeAt(1)); //输出"101" 返回字符编码
alert(stringValue[1]); //"e" 字符串数组
var result = stringValue.concat("world","!"); //result为"hello world!" 但我们更多的是直接 + 拼接字符串
// 正值 slice()、 substr()和 substring()
var stringValue = "hello world";
alert(stringValue.slice(3)); //"lo world"
alert(stringValue.substring(3)); //"lo world"
alert(stringValue.substr(3)); //"lo world"
alert(stringValue.slice(3, 7)); //"lo w"
alert(stringValue.substring(3,7)); //"lo w"
alert(stringValue.substr(3, 7)); //"lo worl"
````
在传递给这些方法的参数是负值的情况下，它们的行为就不尽相同了。
其中， slice()方法会将传入的负值与字符串的长度相加， substr()方法将负的第一个参数加上字符串的长度，而将负的第二个
参数转换为 0。最后， substring()方法会把所有负值参数都转换为 0。下面来看例子。 
大部分场景下记住一个负数参数即可,特殊场景mdn查询
````js
var stringValue = "hello world";
alert(stringValue.slice(-3)); //"rld"
alert(stringValue.substring(-3)); //"hello world"
alert(stringValue.substr(-3)); //"rld"
alert(stringValue.slice(3, -4)); //"lo w"
alert(stringValue.substring(3, -4)); //"hel"
alert(stringValue.substr(3, -4)); //""（空字符串）
````
ECMAScript 5 为所有字符串定义了 trim()方法。这个方法会创建一个字符串的<strong>副本</strong>，删除前置及后缀的所有空格，然后返回结果。  
大小写转换: toLowerCase()、 toLocaleLowerCase()、 toUpperCase()和 toLocaleUpperCase()。  
String 类型定义了几个用于在字符串中匹配模式的方法。第一个方法就是 match(),另一个用于查找模式的方法是 search()。(详见MDN)  
替换子字符串的操作: replace()
分割: split()
#### URI编码
encodeURI()不会对本身属于 URI 的特殊字符进行编码，例如冒号、正斜杠、问号和井字号；而 encodeURIComponent()则会对它发现的任何非标准字符进行编码。来看下面的例子
````js
var uri = "http://www.wrox.com/illegal value.htm#start";
alert(encodeURI(uri)); // "http://www.wrox.com/illegal%20value.htm#start"
alert(encodeURIComponent(uri)); //"http%3A%2F%2Fwww.wrox.com%2Fillegal%20value.htm%23start"
````
解码: decodeURI()和decodeURIComponent()
#### Math
````js
var values = [1, 2, 3, 4, 5, 6, 7, 8];
var max = Math.max.apply(Math, values); // apply第一个参数可以使window null等
````
 Math.ceil()执行向上舍入，即它总是将数值向上舍入为最接近的整数；  
 Math.floor()执行向下舍入，即它总是将数值向下舍入为最接近的整数；  
 Math.round()执行标准舍入，即它总是将数值四舍五入为最接近的整数  
Math.random()方法返回大于等于 0 小于 1 的一个随机数  
套用下面的公式，就可以利用 Math.random()从某个整数范围内随机选择一个值。  
值 = Math.floor(Math.random() * 可能值的总数 + 第一个可能的值)  
举例来说，如果你想选择一个 1到 10 之间的数值，可以像下面这样编写代码：var num = Math.floor(Math.random() * 10 + 1);  
如果想要选择一个介于 2 到 10 之间的值，就应该将上面的代码改成这样：var num = Math.floor(Math.random() * 9 + 2);  
从 2 数到 10 要数 9 个数，因此可能值的总数就是 9，而第一个可能的值就是 2。  
````js
function selectFrom(lowerValue, upperValue) { //通用方法 介于几到几间的一个整数
  var choices = upperValue - lowerValue + 1;
  return Math.floor(Math.random() * choices + lowerValue);
}
var num = selectFrom(2, 10);
alert(num); // 介于 2 和 10 之间（包括 2 和 10）的一个数值

var colors = ["red", "green", "blue", "yellow", "black", "purple", "brown"];
var color = colors[selectFrom(0, colors.length-1)];
alert(color); // 可能是数组中包含的任何一个字符串
````
### 对象
#### Object.defineProperty()
这个方法接收三个参数：属性所在的对象、属性的名字和一个描述符对象。  
其中，描述符（descriptor）对象的属性必须是：configurable、 enumerable、 writable 和 value。
````js
var book = {
  _year: 2004,
  edition: 1
};
Object.defineProperty(book, "year", { // 数据实现双向绑定的基础
  get: function(){
    return this._year;
  },
  set: function(newValue){
    if (newValue > 2004) {
      this._year = newValue;
      this.edition += newValue - 2004;
    }
  }
});
book.year = 2005;
alert(book.edition); //2
````
由于为对象定义多个属性的可能性很大,ECMAScript 5 又定义了一个 Object.defineProperties()方法。利用这个方法可以通过描述符一次定义多个属性。  
  
使用 ECMAScript 5 的 Object.getOwnPropertyDescriptor()方法，可以取得给定属性的描述符。  
这个方法接收两个参数：属性所在的对象和要读取其描述符的属性名称。返回值是一个对象，如果是访问器属性，这个对象的属性有 configurable、 enumerable、 get 和 set；如果是数据属性，这个对象的属性有 configurable、 enumerable、 writable 和 value。
##### 工厂函数





















































