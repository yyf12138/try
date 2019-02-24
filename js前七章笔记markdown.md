## 第一章 JS简介
1.  JavaScript是一种专门为网页交互而设计的脚本语言，有下列不同的三个部分组成：
- ECMAScript,由ECMA-262定义，提供核心语言功能
- 文档对象模型（DOM）,提供访问和操作网页内容的方法和接口
- 浏览器对象模型（BOM）,提供与浏览器交互的方法和接口
2. JavaScript的这三个组成部分，在当前五个主要浏览器（IE、Firefox、Chrome、Safari和Opera）中都得到了不同程度的支持。其中，所有浏览器对ECMAScript第三版的支持大体上都还不错，而对ECMAScript5的支持程度越来越高，但对DOM的支持则彼此相差比较多。对已经正式纳入HTML5标准的BOM来说，尽管各浏览器都实现了某些众所周知的共同特性，但其他特性还是会因浏览器而异。
## 第二章 在HTML中使用JavaScript
1.使用 <script>元素：直接在页面中嵌入JavaScript代码和包含外部JavaScript文件。
- **在使用<script>嵌入JavaScript代码时，只须为<script>指定type属性**。例如:


     <script type="text/javascript">
         function sayHi(){
             alert("Hi!");
         }
     </script>
包含在<script>元素内部的JavaScript代码将被从上至下依次解释。
- **在使用<script>嵌入JavaScript代码时，不要在代码中的任何地方出现“</script>”字符串。**
- **通过<script>元素来包含外部JavaScript文件时，src属性是必须的**。这个属性的值是指向外部javascript文件的一个链接，例如：


     <script type="text/javascript" src="example.js">
     </script>     
- **通过<script>元素的src属性还可以包含来自外部域的javascript文件**。即可以指向当前HTML页面所在域之外的某个域中的完整URL,例如：


     <script type="text/javascript" src="http://www.somewhere.com/afile.js">
     </script>
无论如何包含代码，只要不存在defer和async属性，浏览器都会按照<script>元素在页面中出现的先后顺序对它们依次进解析。
2. 标签的位置。
- **传统的做法，所有的<script>元素都放在<head>元素中**，例如：


     <head>
        <title>aaa</title>
          <script type="text/javascript" src="example.js"></script>
     </head>
- **为了避免浏览器在呈现页面时出现明显的延迟，现代web应用程序一般都把全部JavaScript引用放在<body>元素中页面内容的后面**，例如：


     <head>
        <title>aaa</title>
     </head>
     <body>
     <script type="text/javascript" src="example.js"></script>
     </body>
3.<noscript>元素。符合下述任何一个条件，浏览器都会显示<noscript>中的内容，除此之外其他情况下都不会呈现：
浏览器不支持脚本或是浏览器支持脚本，但脚本被禁用。
## 第三章 基本概念
1. 语法：ECMAScript的语法大量借鉴了C及其他类C语言（如Java和Perl）的语法。
2. 标识符：所谓标识符，就是指变量、函数、属性的名字，或者函数的参数。标识符可以是按照下列格式规则组合起来的一或多个字符：
- 第一个字符必须是一个字母、下划线或一个美元符号（$）；
- 其他字符可以是字母、下划线、美元符号或数字。
3. 变量：ECMAScript的变量是松散类型的，就是可以用来保存任何类型的数据。定义变量时使用var操作符（注意var是一个关键字），后跟变量名（即一个标识符）。
- 用var操作符定义的变量将成为定义该变量的作用域中的**局部变量**。也就是说，如果在函数中使用var定义一个变量，那么这个变量在函数退出后就会被销毁，例如：


     function test(){
         var message = "hi";//局部变量
     }
     test();
     alert(message);//错误！
- 省略var操作符，创建一个**全局变量**：


     function test(){
         message = "hi";//全局变量
     }
     test();
     alert(message);//"hi"
在严格模式下，不能定义名为eval或arguments的变量，否则会导致语法错误。
4. **数据类型：Undefined、Null、Boolean、Number和String。还有一种复杂数据类型---Object,Object本质上是由一组无序的名值对组成的**。
###### typeof操作符--检测给定变量的数据类型
 对一个值使用typeof操作符可能返回下列某个字符串：
- "undefined"-----如果这个值未被定义；
- "boolean"-----如果这个值是布尔值；
- "string"-----如果这个值是字符串；
- "number"-----如果这个值是数值；
- "object"-----如果这个值是对象或null;
- "function"-----如果这个值是函数；
###### Undefined类型
Undefined类型只有一个值，即特殊的undefined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined,例如：


     var message;
     alert(message==undefined);//true
即便未初始化的变量会自动被赋予undefined值，但显式地初始化变量依然是名值的选择。如果能够做到这一点，那么当typeof操作符返回undefined值时我们就知道被检测的变量还没有被声明，而不是尚未初始化
###### Null类型
Null类型是第二个只有一个值的数据类型，这个特殊的值是null。从逻辑角度来看，null值表示一个空对象指针，而这也正是使用typeof操作符检测null值时会返回"object"的原因，例如：


     var car = null;
     alert(typeof car);//"object"
###### Boolean类型
Boolean类型只有两个字面值：true和false(注意不是Ture、False)。这两个值与数字值不是一回事，因此true不一定等于1，而false也不一定等于0。要将一个值转换其对应Boolean值，可以调用转型函数Boolean(),如下例所示：


     var message = "hello world!";
     var messageAsBoolean = Boolean(message);
###### Number类型
- 最基本的数值字面量格式是十进制整数


     var intNum = 55;//整数
- 八进制字面值的第一位必须是零（0），然后是八进制数字序列（0~7）。如果字面值中的数值超出了范围，那么前导零将被忽略，后面的数值将被当做十进制数值解析，例如：


     var Num1 = 070;  //八进制的56
     var Num2 = 079;  //无效的八进制数值--解析为79
     var Num3 = 08;  //无效的八进制数值--解析为8
- 十六进制字面值的前两位必须是0x，
后跟任何十六进制数字（0~9及 A~F)，其中，字母A~F可以大写，也可以小写。例如：


     var Num1 = 0xA;  //十六进制的10
     var Num2 = 0x1f; //十六进制的31
在进行算数计算时，所有以八进制和十六进制表示的数值，最终都将被转换为十进制数值。
- 浮点数值：所谓浮点数值，就是该数值中必须包含一个小数点，并且小数点后面必须至少有一位数字。
 

     var floatNum1 =1.1; 
     var floatNum2=0.1；
     var floatNum3=.1；  //有效，但不推荐
由于保存浮点数值需要的内存空间是保存整数值的两倍，因此ECMAScript会不失时机地将浮点数值转换为整数值。对于那些极大或极小的数值，可以用e表示法（及科学计数法）表示的浮点数值表示。
- NaN:NaN，及非数值（Not a Number)是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误）。NaN本身有两个非同寻常的特点。首先，任何涉及NaN的操作（例如NaN/10)都会返回NaN，这个特点在多步计算中可能导致问题。其次，NaN与任何值都不相等，包括NaN本身。例如，下面的代码会返回false:


     alert(NaN==NaN);  //false
针对NaN的这两个特点，ECMAScript定义了isNaN()函数。isNaN()在接受到一个值后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，例如字符串“10”或Boolean值。而任何不能被转换为数值的值都会导致这个函数返回true。例如：

     alert(isNaN(NaN))；  //true
     alert(isNaN(10));   //false(10是一个数值)
     alert(isNaN（“10”）)；  //false(可以被转换成数值)
- 数值转换：Number()、parseInt()和parseFloat()。第一个函数即转型函数Number()可以用于任何数据类型，而另外两个函数则专门用于把字符串转换成数值。这3个函数对于同样的输入会有返回不同的结果。
- Number()函数的转换规则如下
- [ ] 如果是Boolean值，true和false将分别被转换为1和0.
- [ ] 如果是数字值，只是简单的传入和返回。
- [ ] 如果是null值，返回0。
- [ ] 如果是undefined，返回NaN。
- [ ] 如果是字符串，遵循下列规则：
- 如果字符串中只包含数字（包括数字前面带正号或负号的情况），则将其转换为十进制数值，即“1”会变成1，“123”会变成123，而“011”会变成11（注意：前导的零被忽略了）；
- 如果字符串中包括有效的浮点格式,如“1.1”，则将转换为对应的浮点数值（同样，也会忽略前导零）；
- 如果字符串中包含有效的十六进制格式，例如"oxf",则将其转换为相同大小的十进制整数值。
- 如果字符串是空的（不包含任何字符），则将其转换为0；
- 如果字符串中包含除上述格式之外的字符，则将其转换为NaN。
- [ ] 如果是对象，则调用对象的valueof()方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的tostring()方法，然后再次依照前面的规则转换返回的字符串值。
- parseInt()函数在转换字符串时，更多的是看其是否符合数值模式。如果第一个字符不是数字字符或者负号，parseInt()就会返回NaN；也就是说，用parseInt()转换空字符串会返回NaN(Number()对空字符返回0）。如果第一个字符是数字字符，parseInt()会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。如果字符串中的第一个字符是数字字符，parseInt()也能够识别出各种整数格式（即前面讨论的十进制、八进制和十六进制数）。也就是说，如果字符串一“ox”开头且后跟数字字符，就会将其当作一个十六进制整数；如果字符串以“0”开头且后跟数字字符，则会将其当作一个八进制数来解析。为了更好地理解parseInt()函数的转换规则，下面给出一些例子：


     var num1 = parseInt("1234blue")；  //1234
     var num2 = parseInt("");           //NaN
     var num3 = parseInt("oxA")；        //10(十六进制数)
     var num4 = parseInt("22.5")；     //22
     var num5 = parseInt("070");       //56(八进制数)
     var num6 = parseInt("70")；       //70（十进制数）
在使用parseInt()解析像八进制字面量的字符串时，ECMAScript3和5存在分歧。例如：//ECMAScript  3认为是56（八进制），ECMAScript  5认为是70（十进制）

     var num = parseInt("070")；
与 parseInt()函数类似， parseFloat()也是从第一个字符（位置0）开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。举例来说：“22.34.5”将会被转换为22.34。除了第一个小数点有效之外，parseFloat()与parseInt()的第二个区别在于它始终都会忽略前导的零。parseFloat()可以识别前面讨论过的所有浮点数值格式，也包括十进制整数格式。但十六进制格式的字符串则是总会被转换成0。由于parseFloat()只解析十进制值，因此它没有第二个参数指定基数的用法。最后还要注意一点：如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后都是零），parseFloat()会返回整数。例如：

     var unm1 = parseFloat("1234blue");  //1234(整数)
     var unm2 = parseFloat("0xA");  //0
     var unm3 = parseFloat("22.5");  //22.5
     var unm4 = parseFloat("22.34.5");  //22.34
     var unm5 = parseFloat("0908.5");  //908.5
     var unm6 = parseFloat("3.125e7");  //31250000
- 操作符
- 一元操作符：只能操作一个值的操作符叫做一元操作符。
- 递增和递减操作符：递减和递增操作符直接借鉴自C,而且各有两个版本：前置型和后置型。顾名思义，前置型应该位于要操作的变量之前，后置型则应该位于要操作的变量之后。因此，在使用前置递增操作符给一个数值加1，要把两个加号（++）放在这个数值变量前面，例如:


     var age = 29;
      ++age;     递减类似
- 在应用于不同的值时，递增和递减操作符遵循下列规则： 
- [ ] 在应用于一个包含有效数字字符的字符串时，先将其转换为数字值，在执行加减1的操作。字符串变量变成数值变量。
- [ ] 在应用于一个不包含有效数字字符的字符串时，将变量的值设置为NaN。字符串变量变成数值变量。
- [ ] 在应用于布尔值false时，先将其转换为0再执行加减1的操作。布尔值变量变成数值变量。
- [ ] 在应用布尔值true时，先将其转换为1再执行加减1的的操作。布尔值变量变成数值变量。
- [ ] 在应用浮点数值时，执行加减1的操作。
- [ ] 在应用于对象时，先调用对象的valueof()方法以取得一个可供操作值。然后对该值应用前述规则。如果结果是NaN,则在调用toString()方法后再应用前述规则，对象变量变成数值变量。
- 一元加和减操作符：一元加操作符以一个加号（+）表示，放在数值前面，对数值不会产生任何影响，如下所示：


     var num = “01”；
     num = +num；   //仍然是25

在对非数值应用一元加操作符时，该操作符会像Number()转型函数一样对这个值执行转换，例如：


     var s1 = "01";
     var s2 = "1.1";
     var s3 = "z";
     var b = false;
     var f =1.1;
     var o = (
         valueof : function() {
             reture -1;
         )
     };
     
     s1 = +s1;   //值变成数值1
     s2 = +s2;   //值变成数值1.1
     s3 = +s3；  //值变成NaN
     b = +b;     //值变成数字0
     f = +f;     //值未变，仍然是1.1
     o = +o;     //值变成数值-1

一元加和减操作符主要应用于基本的算术运算，也可以用于转换数字类型。
- 布尔操作符
- 逻辑非：逻辑非操作符由一个叹号（！）表示，可以应用于ECMAScript中的任何值。逻辑非操作符遵循以下规则：
- [ ] 如果操作数是一个对象，返回false;
- [ ] 如果操作数是一个空字符串，返回true;
- [ ] 如果操作数是一个非空字符串，返回false;
- [ ] 如果操作数是数值0，返回true;
- [ ] 如果操作数是任意非0数值（包括Infinity),返回false;
- [ ] 如果操作数是null,返回true;
- [ ] 如果操作数是NaN,返回true;
- [ ] 如果操作数是underfind,返回true；
- 例如：


     alert(!false);    //true
     alert(!"blue");   //false
     alert(!0);        //true
     alert(!NaN);      //true
     alert(!"");       //true
     alert(!12345);    //false

- 逻辑与：逻辑与操作符由两个和号（&&）表示，有两个操作数，例如：


     var result = true && false;

 逻辑与操作可以应用任何类型的操作数，而不仅仅是布尔值，在有一个操作数不是布尔值的情况下，逻辑与操作就不一定返回布尔值；此时’它遵循下列规则：
- [ ] 如果第一个操作数是对象，则返回第二个操作数；
- [ ] 如果第二个操作数是对象，则返回null;
- [ ] 如果有一个操作数是null.则返回null;
- [ ] 如果有一个操作数是NaN,则返回NaN;
- [ ] 如果有一个操作数是underfind,则返回underfind.
- 逻辑或：逻辑或操作符由两个竖线负号（||）表示，有两个操作数，例如


     vae result = true || false

与逻辑与操作相似，如果有一个操作数不是布尔值，逻辑或也不一定返回布尔值；此时，它遵循下列规则：
- [ ] 如果第一个操作数是对象，则返回第一个操作数；
- [ ] 如果第一个操作数的求值结果为false，则返回第二个操作数。
- [ ] 如果两个操作数都是对象，则返回第一个操作数；
- [ ] 如果两个操作数都是null，则返回null;
- [ ] 如果两个操作数都是NaN,则返回NaN;
- [ ] 如果两个操作数都是underfind,则返回undefind;
- 乘性操作符：ECMAScript定义了3个乘性操作符：乘法、除法和求模。
- 乘法：乘法操作符由一个星号（*）表示，用于计算两个数值乘积。其语法类似于C，例如：
 

     var result = 34 * 56;
- 除法：除法操作符由一个斜线符号（/）表示，执行第二个操作数除第一个操作数的计算，例如：
 

     var result = 66 / 11;

- 求模：求模（余数）操作符由一个百分号（%）表示，用法如下： 
 

     var result = 26 % 5；     //等于1

- 加性操作符
- 加法：加法操作符（+）的用法如下：
 

     var result = 1 + 2；

如果两个操作符都是数值，执行常规的加法计算。
如果有一个操作数是对象、数值或布尔值，则调用它们的toString()方法取得相应的字符串值，然后再应用前面关于字符串的规则。对于nuderfind和null，则分别调用String()函数并取得字符串"undenfind"和"num"。例如：


     var result1 = 5 + 5；    // 两个数值相加
     alert (result1);        // 10
     var result2 = 5 + "5";   //一个数值和一个字符串相加
     alert（result2）；       //"55"

- 减法：减法操作符（-）是另一个极为常用的操作符，其用法如下：
 

     var result = 2 - 1;

- - 关系操作符：小于(<)、大于(>)、小于等于(<=)和大于等于(>=)这几个关系操作符用于对两个值进行比较，比较的规则与我们在数学课上所学的一样。这几个操作符都返回一个布尔值，例如：
 

     var result1 = 5 > 3;   //true
     var result2 = 5 < 3;   //false

- 相等操作符
- 想等和不想等：在ECMAScript中的相等操作符由两个等于符号(==)表示，如果两个操作数相等，则返回true。而不相等操作符由叹号后跟等与号(!=)表示，如果两个操作数不相等，则返回true。
- 全等和不全等：除了在比较之前不转换操作数之外，全等和不全等操作符与相等和不相等操作符没有什么区别。全等操作符由3个等于号(===)表示，它只在两个操作数未经转换就相等的情况下返回true，例如：


     var result1 = ("55" == 55);   //true，因为转换后相等
     var result2 = ("55" === 55);   //false，因为不同的数据类型不相等

- 条件操作符：条件操作符应该算是ECMAScript中最灵活的一种操作符了，而且它遵循与Java中条件操作符相同的语法形式，例如：
 

     variable = bolean_expression ？ true_value : false_value;

- 赋值操作符：简单的赋值操作符由等于号(=)表示，其作用就是把右侧的值赋给左侧的变量，例如：
 

     var num = 10;

每个主要算术操作符（以及其他个别的操作符）都有对应的复合赋值操作符。这些操作符如下列所示：
- [ ] 乘/赋值（*=）；
- [ ] 除/赋值（/=);
- [ ] 模/赋值（%=);
- [ ] 加/赋值（+=);
- [ ] 减/赋值（-=);
- [ ] 左移/赋值（<<=）;
- [ ] 有符号右移/赋值（>>=);
- 例如：


     var unm = 10;
     num += 10;

- 函数：函数对任何语言来说都是一个核心的概念。通过函数可以封装任意多条语句，而且可以在任何地方任何时候调用执行。EMAScript中的函数使用function关键字来声明，后跟一组参数以及函数体。函数的基本语法如下列所示：
 

     function functionName(arg0, arg1,...,argN) (
         statments
     )
以下是函数示例：


     function sayHi(name, message) (
         alter("hello " + name "," + message);
     )

- ECMAScript中的函数在定义时不必指定是否返回值。实际上，任何函数在任何时候都可以通过return语句后跟要返回的值来实现返回值。例如：


     function sum(num1, num2) (
         return num1 + num2；
     )
这个sum()函数的作用是把两个值加起来返回一个结果。
- 一个函数中也可以包含多个return语句，例如：
 

     function diff(num1,num2) {
         if (num1 < num2) {
             return num2 - num1;
         } else {
             return num1 - num2;
         }
     }
这个例子中定义的diff()函数用于计算两个数值的差。如果第一个数比第二个小，则用第二个数减第一个数；否则，用第一个数减第二个数。代码中的两个分支都具有自己的return语句，分别用于执行正确的计算。

- 理解参数：可以向ECMAScript函数传递任意数量的参数，并且可以通过arguments对象来访问这些参数。
##  第4章 变量、作用区域和内存问题
- JavaScript变量可以用来保存两种类型的值：
基本类型值和应用类型值。基本类型的值以下5种基本数据类型：Undefined、Null、Boolean、Number 和 String。基本类型值和应用类型值具有以下特点：
- [ ] 基本类型值在内存中占据固定大小的空间，因此保存在栈内存中；
- [ ] 从一个变量向另一个变量复制基本类型的值，会创建这个值的一个副本；
- [ ] 引用类型的值是对象，保存在堆内存中；
- [ ] 包含引用类型值的变量实际上包含的并不是对象本身，而是指向该对象的指针；
- [ ] 从一个变量向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量最终都指向同一个对象；
- [ ] 确定一个值是哪种基本类型可以使用typoef 操作符，而确定一个值是哪种引用类型可以使用instanceof操作符。
##  第5章 应用类型
引用类型的值（对象）是引用类型的一个实例。在ECMAScript中，引用类型是一种数据结构，用于将数据和功能组织在一起。引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。
- 对象是某个特定引用类型的实例，新对象是使用new操作符后跟一个构造函数来创建的。构造函数本身就是一个函数，只不过该函数是出于创建新对象的目的而定义的。例如：
 

     var person = new object();

- object类型：object 是ECMAScript中使用最多的一个类型。
- 创建 object 实例的方法有两种，第一种是使用new操作符后跟 object 构造函数，例如：
 

     var person = new object();
     person.name = "Nicholas";
     person.age = 29;

另一种方式是使用对象字面量表示法。例如：


     var person = {
         name ："Nicholas",
         age : 29
     };
- 使用对象字面量语法时，如果留空其花括号，则可以定义只包含默认属性和方法的对象，例如：
 

     var person = ()；   //与 new object()相同
     person.name = "Nicholas";
     person.age = 29;

- Array 类型：可以用数组的第一个位置来保存字符串，用第二位置来保存数值，用第三个位置来保存对象，以此类推。而且，ECMAScript数组的大小是可以动态调整的，即可以随着数据的添加自动增长以容纳新增数据。创建数组的基本方式有两种。第一种是使用Array构造函数。例如：
 

     var colors = new Array();

创建数组的第二种基本方式是使用数组字面量表示法。数组字面量由一对包含数组项的方括号表示，多个数组项之间用逗号隔开，如下所示：


     var colors = ["red","blue","green"];
     var name = [];
     var values = [1,2,];//不要这样！这样会创建一个包含2或3项的数组
     var options = [,,,,,]；//不要这样！这样会创建一个包含5或6项的数组

转换方法：所有对象都具有toLocaleString()、toString()和valueof()方法。其中，调用toString()方法会返回由数组中每个值的字符串形成拼接而成的一个以逗号分隔的字符串。而调用valueof()返回的还是数组，如下例：


     var colors = ["red","blue","green"];
     alert(colors.toString());//red,blue,green
     alert(colors.valueof());//red,blue,green
     alert(colors);//red,blue,green

- Date类型：要创建一个日期对象，使用new操作符和Date构造函数即可，如下所示：


     var now = new Date();

- Function类型:函数名实际上是一个指向函数对象的指针，不会与某个函数绑定。如下例：


     function sum (num1, num2) {
         return num1 + num2;
     }

由于函数名仅仅是一个指向函数的指针，因此函数名与包括对象指针的其他变量没有什么不同。换句话说，一个函数可能会有多个名字，如下例：


     function sum (num1, num2) {
         return num1 + num2;
     }
     alert(sum(10,10);//20
     
     var anotherSum = sum;
     alert(anotherSum(10,10));//20
     
     sum = null;
     alert(anotherSum(10,10));//20
     
## 第六章 面向对象的程序设计
- 创建对象：构造函数模式，构造函数可用来创建特定类型的对象。例如：


     function Person(name, age, job){
         this.name = name;
         this.age = age;
         this.job = job;
         this.sayName = function(){
             alert(this.name);
         };
     }
     var person1 = new Person("Nicholas", 29,"Software Engineer");
     var person2 = new Person("Greg", 27, "Doctor");

要创建Person的新实例，必须使用new操作符。用这种方式调用构造函数实际上会经历以下四个步骤：
1. 创建一个新对象；
2. 将构造函数的作用域赋给新对象（因此this就指向了这个新对象）；
3. 执行构造函数中的代码（为这个新对象添加属性）；
4. 返回新对象。
- 继承：JavaScript 主要通过原型链实现继承。原型链的构建是通过将一个类型的实例赋值给另一个构造函数的原型实现的。这样，子类型就能够访问超类型的所有属性和方法，这一点与基于类的继承很相似。原型链的问题是对象实例共享所有继承的属性和方法，因此不适宜单独使用。解决这个问题的技术是借用构造函数，即在子类型构造函数的内部调用超类型构造函数。这样就可以做到每个实例都具有自己的属性，同时还能保证只使用构造函数模式来定义类型。使用最多的继承模式是组合继承，这种模式使用原型链继承共享的属性和方法，而通过借用构造函数继承实例属性。
此外，还存在下列可供选择的继承模式。
- [ ]  原型式继承，可以在不必预先定义构造函数的情况下实现继承，其本质是执行对给定对象的浅复制。而复制得到的副本还可以得到进一步改造。
- [ ] 寄生式继承，与原型式继承非常相似，也是基于某个对象或某些信息创建一个对象， 然后增强对象，最后返回对象。为了解决组合继承模式由于多次调用超类型构造函数而导致的低效率问题，可以将这个模式与组合继承-起使用。
- [ ] 寄生组合式继承，集奇生式继承和组合继承的优点与身，是实现基于类型继承的最有效方式
## 第七章 函数表达式
- 递归：递归函数是在一个函数通过名字调用自身的情况下构成的，如下所示：



     function factorial (num) {
         if(num<=1){
            return 1 ;
         }  else {
              return num * factorial (num-1) ;
         }
     }

- 闭包：闭包是指有权访问另一个面数作用城中的全庭的两数。创建闭包的常见方式，就是在一个函数内部创建另一个函数。 以createComparisonFunction()函数为例：


     function createComparisonFunction(propertyName) {
     return function (objectl, object2) {
         var value1 = object1 [propertyName] ;
         var value2 = object2 [propertyName];

         if (value1 < value2){
             return -1;
         } else if (value1 > value2){
         return 1;
             
         } else {
             return 0;
         };
    }


在函数执行过程中，为读取和写入变量的值，就需要在作用域链中查找变量。来看下面的例子：


     function compare (value1, value2) {
         if (value1 < value2) {
             return - 1 ;
         } else if (value1 > value2) {
             return 1 ;
         } else {
             return 0;
         }
    }
    var result = compare(5, 10);

- 闭包与变量：作用域链的这种配置机制引出了一个值得注意的副作用，即闭包只能取得包含函数中任何变量的最后一个值。别忘了闭包所保存的是整个变量对象，而不是某个特殊的变量。下面这个例子可以清晰地说明这个问题。


     function createFunctions() {
         var result = new Array() ;
         for (var i=0; i < 10; i++) {
             result[i] = function() {
                 return i ;

             };
        }
        return result;
    }

这个函数会返回一个函数数组。表面上看，似乎每个函数都应该返自己的索引值，即位置0的函数返回0,位置1的函数返回1,以此类推。但实际上，每个函数都返回10。因为每个函数的作用城链中都保存着createFunctions()函数的活动对象，所以它们引用的都是同一个变量i。当createFunctions()函数返回后，变量i的值是10,此时每个函数都引用着保存变量i的同-一个变量对象，所以在每个函数内部i的值都是10。 但是，我们可以通过创建另一个匿名函数强制让闭包的行为符合预期，如下所示:



     function createFunctions() {
         var result = new Array() ;
         for (var i=0; i < 10; i++) {
            result[i] = function (num) {
                return function() {
                    return num;

                };
            }(i);
         }
         return result;
     }


JavaScript中的函数表达式和闭包都是极其有用的特性，利用它们可以实现很多功能。不过，因为创建闭包必须维护额外的作用域，所以过度使用它们可能会占用大量内存。



















































