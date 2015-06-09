#建议和技巧——控制台篇

## 编写多行命令
控制台在多行编辑的模式下，你可以像在普通的文本编辑器中那样输入命令。 使用`Shift` + `Enter` 可以输入普通的换行符，而实现多行的编辑。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consolemultiline.png)

当你需要写比较的复杂的JavaScript代码的时候，多行编辑就显得很给力了。当你写完一段代码的时候，直接敲回车就可以运行代码了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consolerun.png)


关于支持保存代码的多行控制台，阅读[snippet](../development_workflow.md#定制-javascript-代码片段)


##快捷键打开审查元素模式
使用`Ctrl` + `Shift` + `C` 或 `Cmd` + `Shift` + `C`可以在DevTools中快速打开审查元素模式。(译注：可能会与系统快捷键冲突)

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_10.pn
g)

[更多：使用控制台](../using_console.md)

##支持console.table 命令

该命令支持以表格的形式输出日志信息。下面为代码示例：

    console.table([{a:1, b:2, c:3}, {a:"foo", b:false, c:undefined}]);
    console.table([[1,2,3], [2,3,4]]);

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consoleg1.png)

`table`方法还可以接收一个`columns`参数用来设置表格列的标题。列参数的格式是一个字符串数组，每个数组元素一次对应着列的标题，如果对应列标题为空，则认为不显示该列。下面的代码定义了列的标题:

    function Person(firstName, lastName, age) {
      this.firstName = firstName;
      this.lastName = lastName;
      this.age = age;
    }

    var family = {};
    family.mother = new Person("Susan", "Doyle", 32);
    family.father = new Person("John", "Doyle", 33);
    family.daughter = new Person("Lily", "Doyle", 5);
    family.son = new Person("Mike", "Doyle", 8);

    console.table(family, ["firstName", "lastName", "age"]);

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/consoleperson.png)

如果你只想显示`firstname`和`lastname`，可以通过下面的方式调用：

    console.table(family, ["firstName", "lastName"]);

[了解table方法更多的使用功能| G+.](https://plus.google.com/u/0/115133653231679625609/posts/PmTC5wwJVEc)(译注：需要翻墙)


##预览对象
通过`log`打印的对象可以直接在控制台中预览。
![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_12.png)

##给控制台设置样式
在上一章我们已经提到过，你可以使用`%c`格式符，来为控制台增加样式：

    console.log("%cBlue!", "color: blue;");

还可以为每一块输出设置样式:

    console.log('%cBlue! %cRed!', 'color: blue;', 'color: red;');

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_13.png)

[不同风格的控制台|G+](https://plus.google.com/115133653231679625609/posts/TanDFKEN9Kn)


##快速清空控制台历史
在DevTools窗口中，使用`Ctrl` + `L`或者`Cmd` + `L` 快捷键可以快速的清空命令行历史记录.当然你也可以在控制台直接调用`clear()`方法。


##成为键盘党
在DevTools窗口中，使用 `?`可以打开通用设置面板，在快捷键一项中可以看到DevTools当前支持的所有快捷键。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_14.png)


##在控制台中直接访问页面元素
在元素面板选择一个元素，然后在控制台输入`$0`,就会在控制台中得到刚才选中的元素。如果页面中已经包含了jQuery，你也可以使用`$($0)`来进行选择。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_15.png)

你也可以反过来，在控制台输出的DOM元素上右键选择`Reveal in Elements Panel`来直接在DOM树种查看。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_16.png)

##使用XPath查询DOM
XPath是一种查询语言，用于从DOM文档中查找node，返回结果可能是一组node，字符串，布尔值或者数字。你可以直接在DevTools的JavaScript控制台中直接使用XPath查询语句。

你可以通过`$x(xpath)`的形式执行一个查询语句，下面的示例展示了如何在页面查询图片元素：
![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_17.png)

此外，这个方法还支持扩展的参数，你可以在第二个参数中传入查询的上下文，例如`$x(xpath, context)`。通过扩展参数，你可以选择特定上下文里的DOM元素。

    var frame = document.getElementsByTagName('iframe')[0].contentWindow.document.body;
    $x('//'img, frame);

*在指定的frame中查找img元素*


##访问最近的控制台结果。
在控制台输入`$_`可以获控制台最近一次的输出结果。继续以XPath表达式查询为例：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_17a.png)

##使用 console.dir
`console.dir(object)`命令可以列出参数object的所有对象属性。下面是的例子展示了body对象的属性：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_18.png)


##在特定iframe中执行JavaScript

在DevTools底部工具栏中有一个下拉列表用来改变当前控制台的上下文环境。当你打开控制台面板的时候，你可以直接在下拉列表中选择一个frame来作为JavaScript的执行环境。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_19.png)

##阻止控制台记录在新页面中被清空
在打开一个新的web页面的时候，你可能希望继续保留之前控制台的操作记录，这时候只需要在控制台右键选择"Preserve Log upon Navigation"，这样在打开新的页面的时候，之前的控制台记录还会保存。（译注：在最新版本的Chrome DevTools中，右键已经去掉该选项，可以直接在控制台上方标签中勾选Perserve log）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_20.png)


##使用 console.time() 和 console.timeEnd() 分析循环的性能
调用`console.time()`开启一个计时器，调用 `console.timeEnd()`关闭计时器，并在终端输出计时器消耗的时间。计时器在分析循环这样的非函数内操作的时候还是蛮有用的。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_21.png)

##使用 console.profile() 和 console.profileEnd()分析程序性能
在DevTools窗口控制台中，调用 `console.profile()`开启一个JavaScript CPU 分析器.结束分析器直接调用 `console.profileEnd()`.


![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_22.png)

*具体的性能分析会在分析器面板中*

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_23.png)

*分析结束后，也可以在命令行中调用console.profiles[]得到。*

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_24.png)


**想了解更多关于控制台的使用技巧，请自觉前往[使用控制台](../using_console.md)一章。**
