# readJS_Advanced-Programming
读javascript高级程序设计笔记

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

