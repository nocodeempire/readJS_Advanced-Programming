# 读javascript高级程序设计笔记
刚开始做前端的时候翻过这本红皮书和犀牛书,差不多都看了一半多,没能坚持看完.现在工作相对清闲.准备看完这两本书.对一些知识点也记录下.
***
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
***
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
***
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
````js
function createPerson(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
    alert(this.name);
  };
  return o;
}
var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
````
可以无数次地调用这个函数创建对象，但却没有解决对象识别的问题（即怎样知道一个对象的类型）  
##### 构造函数
````js
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function(){
    alert(this.name);
  };
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
````
每个实例对象都是Person的实例,但问题每个实例对象上的方法(由于方法也是对象)又都是独立开辟的空间
##### 原型模式
````js
function Person(){  // 下面的Person都是这个构造函数
}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
  alert(this.name);
};
// 或者这么写
/** Person.prototype = {
  constructor : Person,
  name : "Nicholas",
  age : 29,
  job: "Software Engineer",
  sayName : function () {
    alert(this.name);
  }
};
*/
````
使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法。  
但原型有个问题,<strong>假设属性值是一个引用类型,对于这个属性值的修改,会反映到各个实例上</strong>  

  
下面是一些es5的新方法, 看一下下面例子应该就知道是什么意思了
````js
// isPrototypeOf
alert(Person.prototype.isPrototypeOf(person1)); //true
alert(Person.prototype.isPrototypeOf(person2)); //true
// getPrototypeOf
alert(Object.getPrototypeOf(person1) == Person.prototype); //true
alert(Object.getPrototypeOf(person1).name); //"Nicholas"
````
  
hasOwnProperty()方法可以检测一个属性是存在于实例中
````js
var person1 = new Person();
alert(person1.hasOwnProperty("name")); //false
person1.name = "Greg";
alert(person1.name); //"Greg"—— 来自实例
alert(person1.hasOwnProperty("name")); //true
````
  
有两种方式使用 in 操作符：单独使用和在 for-in 循环中使用。在单独使用时,in 操作符会在通过对象能够访问给定属性时返回 true，无论该属性存在于实例中还是原型中。
````js
var person1 = new Person();
alert(person1.hasOwnProperty("name")); //false
alert("name" in person1); //true
````
  
由于 in 操作符只要通过对象能够访问到属性就返回 true， hasOwnProperty()只在属性存在于实例中时才返回 true，因此只要 in 操作符返回 true 而 hasOwnProperty()返回 false，就可以确定属性是原型中的属性。
````js
function hasPrototypeProperty(object, name){
  return !object.hasOwnProperty(name) && (name in object);
}
````
  
Object.keys()这个方法接收一个对象作为参数，返回一个包含所有可枚举属性的字符串数组
````js
var keys = Object.keys(Person.prototype);
alert(keys); //"name,age,job,sayName"
var p1 = new Person();
p1.name = "Rob";
p1.age = 31;
var p1keys = Object.keys(p1);
alert(p1keys); //"name,age
````
如果你想要得到所有实例属性，无论它是否可枚举，都可以使用 Object.getOwnPropertyNames()方法。
````js
var keys = Object.getOwnPropertyNames(Person.prototype);
alert(keys); //"constructor,name,age,job,sayName"
````
Object.keys()和 Object.getOwnPropertyNames()方法都可以用来替代 for-in 循环。   

有一点要<strong>注意</strong>:  
调用构造函数时会为实例添加一个指向最初原型的[[Prototype]]指针，而把原型修改为另外一个对象就等于切断了构造函数与最初原型之间的联系。
````js
function Person(){
}
var friend = new Person();
Person.prototype = {
  constructor: Person,
  name : "Nicholas",
  age : 29,
  job : "Software Engineer",
  sayName : function () {
    alert(this.name);
  }
};
friend.sayName(); //error  个人理解 原型定义后,实例化的对象就已经指向了这个原型,把原型重新定义为一个新的对象,地址变了.先前定义的实例没有指向新对象 所以报错. 跟exports与module.exports 其实一个道理.
````
##### 组合使用构造函数和原型
构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。  
这样,每个实例都会有自己的一份实例属性的副本，但同时又共享着对方法的引用，最大限度地节省了内存。
````js
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ["Shelby", "Court"];
}
Person.prototype = {
  constructor : Person,
  sayName : function(){
  alert(this.name);
  }
}
````
##### 动态原型模式
````js
function Person(name, age, job){
  //属性
  this.name = name;
  this.age = age;
  this.job = job;
  //方法
  if (typeof this.sayName != "function"){
    Person.prototype.sayName = function(){
      alert(this.name);
    };
  }
}
````
所有代码都在构造函数中,对于别的OO语言着而言,显得很清晰. 在实例化对象的时候,如果没有sayName方法则在原型上添加,实例对象有这个方法则不添加,很自由.  
但个人认为对于一般项目这个方法省下的那点内存空间意义不大,还是"组合使用构造函数和原型"的方式更让人容易理解
##### 寄生构造函数模式
````js
function Person(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
    alert(this.name);
  };
  return o;
}
var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName(); //"Nicholas"
````
感觉和工厂模式无区别,每次实例化都会开辟一个新空间.纯理论,暂时想不到它的实际用途.
##### 稳妥构造函数模式
做的项目没那么高的安全指数.. 所以直接略过.
***
#### 原型链
````js
function SuperType(){
  this.property = true;
}
SuperType.prototype.getSuperValue = function(){
  return this.property;
};
function SubType(){
  this.subproperty = false;
}
SubType.prototype = new SuperType(); // 这句是精髓
SubType.prototype.getSubValue = function (){
  return this.subproperty;
};
var instance = new SubType();
alert(instance.getSuperValue()); //true
````
懒的放图片了,就看看代码吧. 其实就是子元素的原型指向了父元素的实例对象, <strong>继承</strong>父元素的各个属性/方法.
##### 原型链的问题
````js
function SuperType(){
  this.colors = ["red", "blue", "green"];
}
function SubType(){
}
//继承了 SuperType
SubType.prototype = new SuperType();
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green,black"
````
包含引用类型值的原型属性会被所有实例共享
##### 借用构造函数
````js
function SuperType(){
  this.colors = ["red", "blue", "green"];
}
function SubType(){
  //继承了 SuperType
  SuperType.call(this);
}
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green"
````
相对于原型链而言，借用构造函数有一个很大的优势，即可以在子类型构造函数中向超类型构造函数传递参数。看下面这个例子。
````js
function SuperType(name){
  this.name = name;
}
function SubType(){
  //继承了 SuperType，同时还传递了参数
  SuperType.call(this, "Nicholas");
  //实例属性
  this.age = 29;
}
var instance = new SubType();
alert(instance.name); //"Nicholas";
alert(instance.age); //29
````
##### 组合继承
思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。  
组合继承最大的问题就是无论什么情况下，都会调用两次超类型构造函数：一次是在创建子类型原型的时候，另一次是在子类型构造函数内部。
````js
function SuperType(name){
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
  alert(this.name);
};
function SubType(name, age){
  //继承属性
  SuperType.call(this, name); //第二次调用 SuperType()
  this.age = age;
}
//继承方法
SubType.prototype = new SuperType(); //第一次调用 SuperType()
SubType.prototype.constructor = SubType; //原书有这行代码,将constructor指向SubType, 我觉得不加也无伤大雅,不清楚加的好处在哪
SubType.prototype.sayAge = function(){
  alert(this.age);
};
var instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
instance1.sayName(); //"Nicholas";
instance1.sayAge(); //29
var instance2 = new SubType("Greg", 27);
alert(instance2.colors); //"red,blue,green"
instance2.sayName(); //"Greg";
instance2.sayAge(); //27
````
##### 原型式继承
ECMAScript 5 通过新增 Object.create()方法规范化了原型式继承。
````js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
};
var anotherPerson = Object.create(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");
var yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");
alert(person.friends); //"Shelby,Court,Van,Rob,Barbie"
````
##### 寄生式继承 略
##### 寄生组合式继承
````js
function inheritPrototype(subType, superType){
  var prototype = object(superType.prototype); //创建对象
  prototype.constructor = subType; //增强对象
  subType.prototype = prototype; //指定对象
}
function SuperType(name){
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
  alert(this.name);
};
function SubType(name, age){
  SuperType.call(this, name);
  this.age = age;
}
inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function(){
  alert(this.age);
};
````
***
#### 闭包
闭包是指有权访问另一个函数作用域中的变量的函数。创建闭包的常见方式，就是在一个函数内部创建另一个函数.(老生常谈,不展开)
#### 模块模式
````js
var singleton = function(){
  //私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){
    return false;
  }
  //特权/公有方法和属性
  return {
    publicProperty: true,
    publicMethod : function(){
      privateVariable++;
      return privateFunction();
    }
  };
}();
````
早几年前做的项目都是企业后台,bootstrap搭的,那时候每个页面对应js都是这么写的.
***
#### BOM
假设没有frame,那么top parent self window 都相同,都是window对象
##### 窗口位置
使用下列代码可以跨浏览器取得窗口左边和上边的位置。
````js
var leftPos = (typeof window.screenLeft == "number") ? window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop == "number") ? window.screenTop : window.screenY;
````
##### 页面视口的大小
````js
  var clientWidth = document.documentElement.clientWidth || document.body.clientWidth;
  var clientHeight = document.documentElement.clientHeight || document.body.clientHeight;
````
##### 导航和打开窗口
使用 window.open()方法既可以导航到一个特定的 URL，也可以打开一个新的浏览器窗口。  
这个方法可以接收 4 个参数：要加载的 URL、窗口目标、一个特性字符串以及一个表示新页面是否取代浏览器历史记录中当前加载页面的布尔值。  
通常只须传递第一个参数，最后一个参数只在不打开新窗口的情况下使用  
新创建的 window 对象有一个 opener 属性，其中保存着打开它的原始窗口对象。这个属性只在弹出窗口中的最外层 window 对象（top）中有定义，而且指向调用 window.open()的窗口或框架.
##### location 对象
它既是 window 对象的属性，也是document 对象的属性；换句话说， window.location 和 document.location 引用的是同一个对象。  

| 属 性 名       | 例 子                       | 说 明                                                                   |
| ------------- |:---------------------------:| -----------------------------------------------------------------------:|
| hash          | "#contents"                 | 返回URL中的hash（#号后跟零或多个字符），如果URL中不包含散列，则返回空字符串   |
| host          | "www.wrox.com:80"           | 返回服务器名称和端口号（如果有）                                           |
| hostname      | "www.wrox.com"              | 返回不带端口号的服务器名称                                                 |
| href          | "http:/www.wrox.com"        | 返回当前加载页面的完整URL。而location对象的toString()方法也返回这个值        |
| pathname      | "/WileyCDA/"                | 返回URL中的目录和（或）文件名                                              |
| port          | "8080"                      | 返回URL中指定的端口号。如果URL中不包含端口号，则这个属性返回空字符串          |
| protocol      | "http:"                     | 返回页面使用的协议。通常是http:或https:                                    |
| search        | "?q=javascript"             | 返回URL的查询字符串。这个字符串以问号开头                                   |

````js
//假设初始 URL 为 http://www.wrox.com/WileyCDA/
//将 URL 修改为"http://www.wrox.com/WileyCDA/#section1"
location.hash = "#section1";
//将 URL 修改为"http://www.wrox.com/WileyCDA/?q=javascript"
location.search = "?q=javascript";
//将 URL 修改为"http://www.yahoo.com/WileyCDA/"
location.hostname = "www.yahoo.com";
//将 URL 修改为"http://www.yahoo.com/mydir/"
location.pathname = "mydir";
//将 URL 修改为"http://www.yahoo.com:8080/WileyCDA/"
location.port = 8080;
//每次修改 location 的属性（hash 除外），页面都会以新 URL 重新加载。
````
***
#### 浏览器检测
1.能力检测  
2.怪癖检测  
3.用户代理检测  
#### DOM
````js
//document.documentElement 整个文档 即<html>....</html>
//document.body 整个body 即<body>....</body>
//document.url 即location.url
//document.domain 
// ...
````
div.tagName 实际上输出的是"DIV"而非"div"。在 HTML 中，标签名始终都以全部大写表示  
取得特性: getAttribute()、 setAttribute()和 removeAttribute()  
...  
scrollIntoView()方法 (除了smooth属性外,现代浏览器几乎都能用了)  
children属性 只包含元素中同样还是元素的子节点  
contains()方法 调用的应该是祖先节点，也就是搜索开始的节点，这个方法接收一个参数，即要检测的后代节点。如果被检测的节点是后代节点，该方法返回 true；否则，返回 false。
##### 偏移量 (只读)
offsetHeight: 元素在垂直方向上占用的空间大小，以像素计。包括元素的高度、（可见的）水平滚动条的高度、上边框高度和下边框高度。  
offsetWidth：元素在水平方向上占用的空间大小，以像素计。包括元素的宽度、（可见的）垂直滚动条的宽度、左边框宽度和右边框宽度。  
offsetLeft：元素的左外边框至包含元素的左内边框之间的像素距离。  
offsetTop：元素的上外边框至包含元素的上内边框之间的像素距离.  
其中， offsetLeft 和 offsetTop 属性与包含元素有关，包含元素的引用保存在 offsetParent属性中.  

<img src="https://images2015.cnblogs.com/blog/896142/201609/896142-20160902100214152-56057312.jpg" />  

##### 客户区大小 (只读)
clientWidth 属性是元素内容区宽度加上左右内边距宽度;  
clientHeight 属性是元素内容区高度加上上下内边距高度。  
从字面上看，客户区大小就是元素内部的空间大小，因此滚动条占用的空间不计算在内。  
<img src="https://pic002.cnblogs.com/images/2011/280254/2011112914113672.png" />  

<strong>所有这些偏移量属性都是只读的，而且每次访问它们都需要重新计算。  
 因此，应该尽量避免重复访问这些属性；如果需要重复使用其中某些属性的值，可以将它们保存在局部变量中，以提高性能。</strong>

##### 滚动大小
 scrollHeight：在没有滚动条的情况下，元素内容的总高度。  
 scrollWidth：在没有滚动条的情况下，元素内容的总宽度。  
 scrollLeft：被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置。  
 scrollTop：被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置。  
<strong>scrollLeft 和 scrollTop这两个属性都是可以设置的，因此将它们设置为 0，就可以重置元素的滚动位置。</strong>  
<img src="https://pic002.cnblogs.com/images/2011/280254/2011112914120887.png" />  

##### 确认元素大小
getBoundingClientRect()方法。这个方法返回会一个矩形对象，包含 4 个属性： left、 top、 right 和 bottom。  
浏览器的实现稍有不同。 IE8 及更早版本认为文档的左上角坐标是(2, 2)，而其他浏览器包括 IE9 则将传统的(0,0)作为起点坐标。  
***
#### DOM事件流
三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段.  
<img src="https://images2015.cnblogs.com/blog/402105/201508/402105-20150825224811297-382732435.png" />  

##### 事件
addEventListener() removeEventListener() 它们都接受 3 个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。  
最后这个布尔值参数如果是 true，表示在捕获阶段调用事件处理程序；如果是 false，表示在冒泡阶段调用事件处理程序。(ie9开始支持)  
event 对象包含与创建它的特定事件有关的属性和方法。  

| 属性方法                     | 类 型         | 说 明                                                                    |
| --------------------------- |:-------------:| ------------------------------------------------------------------------:|
| bubbles                     | Boolean       | 表明事件是否冒泡                                                           |
| cancelable                  | Boolean       | 表明是否可以取消事件的默认行为                                              |
| currentTarget               | Element       | 其事件处理程序当前正在处理事件的那个元素                                     |
| defaultPrevented            | Boolean       | 为true表示已经调用了preventDefault()                                       |
| detail                      | Integer       | 与事件相关的细节信息                                                       |
| eventPhase                  | Integer       | 调用事件处理程序的阶段： 1表示捕获阶段， 2表示“处于目标”， 3表示冒泡阶段       |
| preventDefault()            | Function      | 取消事件的默认行为。如果cancelable是true，则可以使用这个方法                  |
| stopImmediatePropagation()  | Function      | 取消事件的进一步捕获或冒泡，同时阻止任何事件处理程序被调用                     |
| stopPropagation()           | Function      | 取消事件的进一步捕获或冒泡。如果bubbles为true，则可以使用这个方法              |
| target                      | Element       | 事件的目标                                                                 |
| trusted                     | Boolean       | 为true表示事件是浏览器生成的。为false表示事件是由开发人员通过JavaScript创建的  |
| type                        | String        | 被触发的事件的类型                                                          |
| view                        | AbstractView  | 与事件关联的抽象视图。等同于发生事件的window对象                              |

在事件处理程序内部，对象 this 始终等于 currentTarget 的值，而 target 则只包含事件的实际目标。如果直接将事件处理程序指定给了目标元素，则 this、currentTarget 和 target 包含相同的值。  
  

load事件: 当页面完全加载后（包括所有图像、 JavaScript 文件、CSS 文件等外部资源），就会触发 window 上面的 load 事件。  
unload事件: 与 load 事件对应的是 unload 事件，这个事件在文档被完全卸载后触发。  
resize事件: 当浏览器窗口被调整到一个新的高度或宽度时，就会触发 resize 事件。这个事件在 window（窗口）上面触发，因此可以通过 JavaScript 或者<body>元素中的 onresize 特性来指定事件处理程序。  
( IE、 Safari、 Chrome 和 Opera 会在浏览器窗口变化了 1 像素时就触发 resize 事件，然后随着变化不断重复触发。 Firefox 则只会在用户停止调整窗口大小时才会触发 resize 事件。由于存在这个差别，应该注意不要在这个事件的处理程序中加入大计算量的代码，因为这些代码有可能被频繁执行，从而导致浏览器反应明显变慢。浏览器窗口最小化或最大化时也会触发 resize 事件。)  
scroll事件: 虽然scroll事件是在window 对象上发生的，但它实际表示的则是页面中相应元素的变化。 document.documentElement.scrollTop || document.body.scrollTop  
  
##### 焦点事件
焦点事件会在页面元素获得或失去焦点时触发。利用这些事件并与 document.hasFocus()方法及document.activeElement 属性配合，可以知晓用户在页面上的行踪。有6个焦点事件.常用的就focus 和 blur, focusin与focusout  

##### 下面几个位置都是相对鼠标而言的
1.客户区坐标位置  
鼠标事件都是在浏览器视口中的特定位置上发生的。这个位置信息保存在事件对象的 clientX 和clientY 属性中。所有浏览器都支持这两个属性，它们的值表示事件发生时鼠标指针在视口中的水平和垂直坐标。  
2.页面坐标位置  
通过客户区坐标能够知道鼠标是在视口中什么位置发生的，而页面坐标通过事件对象的 pageX 和pageY 属性，能告诉你事件是在页面中的什么位置发生的。换句话说，这两个属性表示鼠标光标在页面中的位置，因此坐标是从页面本身而非视口的左边和顶边计算的.在页面没有滚动的情况下， pageX 和 pageY 的值与 clientX 和 clientY 的值相等。  
3.屏幕坐标位置  
鼠标事件发生时，不仅会有相对于浏览器窗口的位置，还有一个相对于整个电脑屏幕的位置。而通过 screenX 和 screenY 属性就可以确定鼠标事件发生时鼠标指针相对于整个屏幕的坐标信息。  

##### 触摸与手势事件
 touchstart：当手指触摸屏幕时触发；即使已经有一个手指放在了屏幕上也会触发。  
 touchmove：当手指在屏幕上滑动时连续地触发。在这个事件发生期间，调用 preventDefault()可以阻止滚动。  
 touchend：当手指从屏幕上移开时触发。  

##### 表单的一些事件
 blur：当前字段失去焦点时触发。  
 change：对于<input>和<textarea>元素，在它们失去焦点且 value 值改变时触发；对于<select>元素，在其选项改变时触发。  
 focus：当前字段获得焦点时触发。  
change 事件在不同表单控件中触发的次数会有所不同。对于<input>和<textarea>元素，当它们从获得焦点到失去焦点且 value 值改变时，
才会触发 change 事件。对于<select>元素，只要用户选择了不同的选项，就会触发 change 事件；换句话说，不失去焦点也会触发 change 事件。  
selectionStart 和 selectionEnd 这两个属性中保存的是基于 0 的数值，表示所选择文本的范围（即文本选区开头和结尾的偏移量）  
  
除select()方法之外，所有文本框都有一个setSelectionRange()方法。这个方法接收两个参数：要选择的第一个字符的索引和要选择的最后一个字符之后的字符的索引
（类似于 substring()方法的两个参数）。

##### 操作剪贴板 (存在兼容性)
 beforecopy：在发生复制操作前触发。  
 copy：在发生复制操作时触发。  
 beforecut：在发生剪切操作前触发。  
 cut：在发生剪切操作时触发。  
 beforepaste：在发生粘贴操作前触发。  
 paste：在发生粘贴操作时触发。  
这个 clipboardData 对象有三个方法：getData()、setData()和 clearData()。  
































