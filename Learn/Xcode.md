
## Object-C 学习

1. OC相对于C
    a. 在C的基础之上新增了1小部分面向对象的语法
    b. 将C的复杂的、繁琐的、可恶的语法封装的更为简单

    c. OC完全兼容C语言
<div></div>

2. OC程序的源文件的后缀名是.m   m代表message  代表OC中最重要的1个机制  消息机制。   C程序的源文件的后缀名.C
<div></div>

3. main函数仍然是OC程序的入口和出口.
    int类型的返回值 代表程序的结束状态。
    main函数的参数：仍然可以接收用户在运行程序的时候传递数据给程序。参数也可以不要。
<div></div>

4. #import指令。

    1. 以#号开头，是1个预处理指令。
    2. 作用： 是#include指令的增强版，将文件的内容在预编译的时候拷贝写指令的地方。
    3. 增强： 同1个文件无论#import多少次，只会包含一次。
       1. 如果#include指令要实现这个效果，就必须要配合条件编译指令来实现。
       2. 而#import指令只需要直接包含就可以 其他什么都不用做
<div></div>

5. 框架
   1.  是1个功能集  苹果或第三方事先将一些程序在开发程序的时候经常要用到的功能事先写好，把这些功能封装在1个1个的类或者函数之中。这些函数和类的集合叫做框架。
   2.   Foundation框架<br>Foundation: 基础 基本。 这个框架中提供了一些最基本的功能  输入和输出，一些数据类型。<br>Foundation.h的路径<br>/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/System/Library/Frameworks/Foundation.framework/Versions/C/Headers<br><div></div>
   Foundation.h 这个文件中包含了Foundation框架中的其他的所有的头文件。<br>所以，我们只要包含Foundation.h 就相当于包含了Foundation框架中所有的头文件。<br>那么Foundation框架中的所有的函数和类就可以直接使用。
<div></div>

6. @autorelesasepool 是自动释放池
    <br>你只需要知道这个是1个自动释放池
    <br>你可以将代码写在自动释放池之中  或者干脆把这个自动释放池删除    不会有任何影响
<br>

7. NSLog函数
   1. 作用：是print函数的增强版。向控制台输出信息
   2. 语法：<br>$\qquad$NSLog(@"格式控制字符串"，变量列表)；</br><br>最简单的语法:</br>$\qquad$NSLog(@"要输出的信息")；
   3. 增强：
      1. 输出一些调试相关信息。<br>2021-12-14 01:40:09.961623+0000 01-Demo[16764:1171244] Hello, World!<br><br>执行这段代码的时间。<br>程序的名称<br>进程编号<br>线程编号<br>输出的信息。
        <br>
      2. 会自动换行，在输出完信息之后$\qquad$会自动换行。
   <br>
      3. OC中其实新增了一些数据类型。NSLog函数不仅仅可以输出C数据类型变量的值还可以输出OC新增的数据类型的变得值。
    <br>  
      4. 用法和print函数差不多， 一样可以输出变的值 并且占位符和用法都一样
    <br> 
      5. 使用注意：
         1. NSLog函数的第1个参数前面必须要加1个@符号
         2. 如果手贱在字符串的末尾加了1个'\n'代表换行   那么函数的自动换行功能就会失效。

忘记#include 用#import
忘记print 用NSLog
<br>

8. 字符串
   1. C语言的字符串的储存方式
      1. 使用字符数组储存
      2. 使用字符指正
   <br>
   2. OC中设计了1个更为好用的用来储存字符串的1个类型。  NSString<br>Nsstring 类型的指针变量 专门用来储存OC字符串地址。
   
   <br>

   3. OC的字符串常量必须要使用1个前缀@符号<br>"jack" 这是1个C语言的字符串。<br>@"jack" 这是1个OC的字符串常量。<br>NSString类型的指针变量，只能存储OC字符串的地址。<br>NSString *str = @"jack";
   <br>

   4. 总结
      1. 在OC中专门设计了1个NSString类型来储存字符串
      2. 字符串分为C字符串和OC字符串.<br><br>字符串如果没有@前缀 那么这个字符串常量就是1个C字符串。<br>字符串如果没有@前缀  那么这个字符串常量就是OC字符串。<br><br>@"jack"<br>"rose"<br><br>所以，OC字符串常量的前面必须要加1个@符号。
      3. NSString类型的指针变量 只能存储    OC字符串。
   <br>
   5. 注意
      1. NSLog函数的第1个参数是1个OC字符串，所以NSLog函数的第1个实参应该以@符号开头。
      <br>
      2. 如果要使用NSLog函数输出OC字符串的值，那么使用占位符%@
<br>

9. NS前缀
   
   1.  NextStep ---> Cocoa ---> Foundation框架之中。
<br>

10. @符号
    <br>
    1. 将C字符串转换为OC字符串。<br><br>"jack"  @"jack"
    <br>
    2. OC中的绝大部分的关键字都是以@符号开头。
<br>
11. 注释：<br>和C语言的注释一模一样，分单行注释和多行注释<br>单行注释: //<br>多行注释: /* xxx */
<br>
12. 函数的定义和调用<br>与C语言的函数的定义和调用是一样的 
 


   


   
   



