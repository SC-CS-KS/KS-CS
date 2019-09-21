# What Is JavaScript

## ECMAScript
```md
ECMA International是一家国际性会员制度的信息和电信标准组织，它和企业密切相连的组织，
所以 Ecma国际制定的规范标准都是由各类企业来做主要的制定和推广。

1997年该组织发布了MCMA-262的标准，该标准制定了MCMAScript语言规范。
```
* ECMA-262
```md
ECMA-262是ECMA TC39小组制定的关于脚本语言的规范标准。
TC39成员由来自一些对脚本编程感兴趣的公司的程序员组成的。
```
```md
ECMA-262标准定义了ECMAScript语言规范。
这个这个标准也叫成为ECMAScript语言规范(ECMAScript Language Specification)，简称ES规范。
```
```md
截至 2012 年，所有的现代浏览器都完整了支持 ECMAScript 5.1，旧式的浏览器至少支持 ECMAScript 3 标准。
在2015年6月17日，ECMA国际组织发布了 ECMAScript 的第六版，该版本正式名称为ECMAScript 2015，
但通常被称为 ECMAScript 6 或者ES6。
自此，ECMAScript每年发布一次新标准。
```
## JavaScript 标准化
```md
1995年前后，互联网爆发，Web应用层出不穷。就在那时候 JavaScript 有三个主流版本：
1. Netscape Navigator 3.0 中的 JavaScript
2. IE 中的 JScript
3. CEnvi 中的ScriptEase。

与和其他编程语言不同的是，JavaScript 并没有一个标准来统一其语法或特性，而这 3 种不同的版本恰恰突出了这个问题。
随着业界担心的增加，这个语言的标准化显然已经势在必行。
```
```md
1997年，JavaScript 1.1 作为一个草案提交给欧洲计算机制造商协会（ECMA）。
第 39 技术委员会（TC39）被委派来“标准化一个通用、跨平台、中立于厂商的脚本语言的语法和语义”。
锤炼出了 ECMA-262第一版，该标准定义了名为 ECMAScript 的全新脚本语言。
```
```md
1998年，国际标准化组织及国际电工委员会（ISO/IEC）也采纳 ECMAScript 作为标准（ISO/IEC-16262）。
同年发布了ECMA-262第二个版(ES2)。第二个版本基本没有加新功能。
```
```md
2002年 ECMA-262第三版(ES3)，ECMA-262第4版本(ES4)夭折，部分功能被迁移到ES6中。
2009年 ECMA-262第五版(ES5)发布。
2011年 被批准为国际标准iso / iec 16262：2011。同年发布ES5.1版本(对ES5做一些升级优化)同时被MCMA-262和ISO/IEC批准。
2015年 ECMA-262第六版(ES6或者叫ES 2015语言规范)，
    ES6可以说从2000年，ES3发布之后就开始沉淀，由于ES4的夭折，
    ES4中的一些功能特性一直等到ES6才发布，所以第六版的完全是十五年的努力的结果。
```
* ES6
```md
ES6为大型应用程序提供更好的支持，创建Lib库，以及使用ECMAScript作为其他语言的编译目标。
```
## JavaScript vs ECMAScript
```md
JavaScript是ECMAScript的一种实现（分支），遵循ECMAScript标准。
目前主流浏览器已经可以完美兼容和使用ES6。

换句话说就是ECMAScript的方言，其他的还有微软的jscript等。
```

## JS 的实现包含三个方面：
```md
1. ECMAScript(语言核心功能基于ES规范)
2. DOM— js需要支持对DOM的维护，通过document，element对象实现。这些都是在ES中没有的。
3. BOM— js需要支持对BOM的维护，通过window对象实现。这些都是在ES中没有的。
```

## JS 必须学习三分方面的知识：
```md
1.ES5/ES6语法。
2.用第一部分学的语法，通过DOM对象提供的属性方法来操作DOM。
3.用第一部分学的语法，通过BOM对象提供的属性方法来操作BOM。
```

## VS 浏览器
* 浏览器性能差异
```md
与JavaScript引擎的实现方式有关系。
```
* 浏览器支持差异
```md
多种不同的JS引擎处理同一份JS代码会存在差异，这种差异是处理引擎造成的，
有的浏览器支持，有的浏览器不支持，这就造成兼容性的问题。
```

## [JavaScript语言的历史](http://javascript.ruanyifeng.com/introduction/history.html)
