#使用控制台

利用控制台可以做如下的事情：

+ 日志诊断信息帮助你调试web应用。
+ 输入命令和页面或DevTools进行交互

你要可以在里面执行普通的表达式。本文将介绍控制台的概要以及基本的一些使用。你可以浏览[Console API](https://developer.chrome.com/devtools/docs/console-api)和[Command line API](https://developer.chrome.com/devtools/docs/commandline-api)参考手册了解更多的功能。


##基本操作

###打开命令行
JavaScript 控制台可以通过两种方式打开。常用的方式是打开控制台面板,当然你可以在其他面板中随时点击右上角的控制台图标弹出抽屉窗口:

+ 使用快捷键 `Command` + `Option` + `J`(Mac) 或者`Control` + `Shift` + `J` (Windows/Linux)。
+ 选择Chrome菜单 > 更多工具 > JavaScript 控制台.

![](https://developer.chrome.com/devtools/docs/console-files/console1.png)

*一个清空的抽屉界面*

要打开控制台，可以按`Esc`键或单击DevTools窗口右上角的显示控制台按钮。

![](https://developer.chrome.com/devtools/docs/console-files/console-in-drawer.png)

*在元素面板中打开的控制台界面*


###清空控制台历史记录
可以通过下面的方式清空控制台历史：

+ 在控制台右键，或者按下`Ctrl`并单击鼠标，选择`Clear Console`。
+ 在脚本窗口输入`clear()`执行。
+ 在JavaScript脚本中调用`console.clear()`。
+ 使用快捷键 `Cmd` + `K`, `^` + `L` (Mac) `Ctrl` + `L` (Windows and Linux)。

###消息栈
控制台会默认的折叠连续输出相同内容的消息，这样使得输出尽可能的保持简洁。

![](https://developer.chrome.com/devtools/docs/console-files/timestamps-disabled.png)

*默认情况下,隐藏时间戳，折叠消息*

![](https://developer.chrome.com/devtools/docs/console-files/timestamps-enabled.png)

*取消消息折叠(译注：该功能可以在DevTools设置中修改，点击右上角齿轮图标)*

下面的代码可以用来测试折叠消息的效果

    msgs = ['hello', 'world', 'there'];
    for (i = 0; i < 20; i++) console.log(msgs[Math.floor((i/3)%3)])


###Frame 选择
控制台支持在不同的frame中进行操作。主页面默认为top frame。一个`iframe`元素会创建自己的上下文环境，你可以从下拉列表中自由的选择frame。

![](https://developer.chrome.com/devtools/docs/console-files/frame-selection.png)


*选择一个二级frame*

![](https://developer.chrome.com/devtools/docs/console-files/locations-between-frames.png)

*上图显示了再切换frame时，window origin属性的变化*



##使用 Console API
Console API 就是DevTools定义的全局变量`console`对象的方法集合。API的主要目的在于当你的程序运行时为你记录日志信息。你还可以对输出进行分类，使日志看起来更加清晰。

###向控制台输出

`console.log()`方法可以接受一个或多个表达式作为参数，并将他们的值打印到控制台。

下面一段代码演示了基本的使用：

    var a = document.createElement('p');
    a.appendChild(document.createTextNode('foo'));
    a.appendChild(document.createTextNode('bar'));
    console.log("Node count: " + a.childNodes.length);

![](https://developer.chrome.com/devtools/docs/console-files/log-basic.png)
*上面代码的输出结果*

当有多个参数的时候，结果会拼接成连续的一行。

下面代码为`console.log()`接受多个参数：

    console.log("Node count:", a.childNodes.length, "and the current time is:", Date.now());

![](https://developer.chrome.com/devtools/docs/console-files/log-multiple.png)
*多参数的输出*


### 错误和警告
错误和警告信息和普通输出一样使用。区别在于其输出的样式不同，`console.error()`打印的结果是红色的，`console.warn()`打印的信息是黄色的。

*error()使用代码及结果*

    function connectToServer() {
        console.error("Error: %s (%i)", "Server is  not responding",500);
    }
    connectToServer();

![](https://developer.chrome.com/devtools/docs/console-files/error-server-not-resp.png)


*warn()使用代码及结果*

    if(a.childNodes.length < 3 ) {
        console.warn('Warning! Too few nodes (%d)', a.childNodes.length);
    }

![](https://developer.chrome.com/devtools/docs/console-files/warning-too-few-nodes.png)


###断言
`console.assert()`接受两个参数，如果第一个参数的结果为`false`，则该方法会将第二个参数输出到控制台。

下面的代码会判断list元素的子节点数目是否超过500，如果超过则打印一条错误消息：
    
    console.assert(list.childNodes.length < 500, "Node count is > 500");

![](https://developer.chrome.com/devtools/docs/console-files/assert-failed.png)



###过滤输出
你可以根据级别对日志输出进行过滤。点击界面左上角的漏斗形状的图标即可对日志进行过滤,目前支持的日志级别包括：

+ All - 显示所有的输出
+ Errors - 只显示 console.error() 的输出
+ Warnings - 只显示 console.warn()的输出
+ Info - 只显示 console.info()的输出
+ Logs - 只显示 console.log()的输出
+ Debug - 只显示 console.timeEnd() 和 console.debug()的输出

![](https://developer.chrome.com/devtools/docs/console-files/filter-errors.png)

###分组输出

你可以使用group命令对相关的输出进行分组。`group`方法只接受一个字符串参数，表示分组的名称。控制台会把接下来所有的输出组合输出，调用`groupEnd()`可以结束当前分组.

下面的代码演示了如何进行分组输出：

    var user = "jsmith", authenticated = false;
    console.group("Authentication phase");
    console.log("Authenticating user '%s'", user);
    // authentication code here...
    if (!authenticated) {
        console.log("User '%s' not authenticated.", user)
    }
    console.groupEnd();

![](https://developer.chrome.com/devtools/docs/console-files/group.png)

日志分组是可以相互嵌套的，当分组信息较多的时候比较有用，下面代码显示了分组嵌套的例子：

    var user = "jsmith", authenticated = true, authorized = true;
    // Top-level group
    console.group("Authenticating user '%s'", user);
    if (authenticated) {
        console.log("User '%s' was authenticated", user);
        // Start nested group
        console.group("Authorizing user '%s'", user);
        if (authorized) {
            console.log("User '%s' was authorized.", user);
        }
        // End nested group
        console.groupEnd();
    }
    // End top-level group
    console.groupEnd();
    console.log("A group-less log trace.");

![](https://developer.chrome.com/devtools/docs/console-files/nestedgroup.png)

当日志量较大的时候，可能并不需要看到所有的日志信息，这时推荐使用[groupCollapsed()](https://developer.chrome.com/devtools/docs/console-api#consolegroupcollapsed)方法，该方法会默认折叠同组的信息。

代码示例：

    console.groupCollapsed("Authenticating user '%s'", user);
    if (authenticated) {
        ...
    }
    console.groupEnd();

![](https://developer.chrome.com/devtools/docs/console-files/groupcollapsed.png)


###查看数据结构
`table()`方法可以用来查看对象的内容。该方法会将对象的属性以表格的形式打印出来。

下面代码显示了打印两个数组的内容：

    console.table([{a:1, b:2, c:3}, {a:"foo", b:false, c:undefined}]);
    console.table([[1,2,3], [2,3,4]]);

![](https://developer.chrome.com/devtools/docs/console-files/table-arrays.png)

`table()`的第二个参数是可选的，你可传入一个字符串数组，来指定想显示的属性。

示例代码如下：

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

![](https://developer.chrome.com/devtools/docs/console-files/table-people-objects.png)

###字符串裁剪和格式化
日志输出一系列方法的第一个字符串参数都可以包含一个或者多个格式符。格式符由`%`后面跟一个字母组成，字母代表不同的格式。每个格式符与后面的参数一一对应。

下面的例子中，日志打印了结果中包含了字符串格式和数字格式内容。

    console.log("%s has %d points", "Sam", 100);

The full list of format specifiers are as follows:

+ %s - 字符串格式
+ %i 或 %d - 整型格式
+ %f - 浮点格式
+ %o - DOM节点
+ %O - JavaScript 对象
+ %c - 对输出的字符串使用css样式，样式由第二个参数指定。

下面的例子使用整型来打印 `document.childNodes.length`的值，使用浮点格式来打印`Date.now()`的值。

    console.log("Node count: %d, and the time is %f.", document.childNodes.length, Date.now());

###将DOM与元素格式化为JavaScript对象
当你打印一个DOM元素的时候，它会以XML的格式显示，正如在元素面板中看到的那样。如果要以JavaScript对象的形式显示，你可以使用`dir()`方法或者在`log()`中制定格式符。

![](https://developer.chrome.com/devtools/docs/console-files/log-element.png)
*默认情况打印DOM元素*

![](https://developer.chrome.com/devtools/docs/console-files/dir-element.png)
*使用dir打印*


###使用CSS增加控制台样式
CSS格式符允许你自定义控制台输出的样式。第二个参数可以制定具体的样式。

代码演示：

    console.log("%cThis will be formatted with large, blue text", "color: blue; font-size: x-large");

![](https://developer.chrome.com/devtools/docs/console-files/format-string.png)


###耗时监控
通过调用`time()`可以开启计时器。你必须传入一个字符串参数来唯一标记这个计时器的ID。当你要结束计时的时候可以调用`timeEnd()`，并且传入指定的名字。计时结束后控制台会打印计时器的名字和具体的时间。

代码示例：

    console.time("Array initialize");
        var array= new Array(1000000);
        for (var i = array.length - 1; i >= 0; i--) {
            array[i] = new Object();
        };
    console.timeEnd("Array initialize");

![](https://developer.chrome.com/devtools/docs/console-files/time-duration.png)

如果在计时期间正好有[timeline](https://developer.chrome.com/devtools/docs/timeline)操作。`time()`则也会显示在timeline上。这可以帮你更加清晰的看到耗时到底在哪里。

![](https://developer.chrome.com/devtools/docs/console-files/time-annotation-on-timeline.png)


###标注 Timeline
在 Timeline 面板，你可以看到浏览器引擎的耗时分布。你可以通过调用`timeStamp()`方法在Timeline中打上一个标记。通过这样的方式你可以看到不同事件之间的联系。

> 注意：`timeStamp()`方法只有在timeline记录期间生效。

Timeline中标记的结果会通过两种方式显示：

+ Timeline中的显示一个黄色的竖线
+ 事件列表中新增一个事件

代码示例：

    function AddResult(name, result) {
    console.timeStamp("Adding result");
    var text = name + ': ' + result;
    var results = document.getElementById("results");
    results.innerHTML += (text + "<br>");
    }

![](https://developer.chrome.com/devtools/docs/console-files/timestamp2.png)


###在JavaScript代码中设置断点

在代码中插入 `debugger;`语句相当于在相应的代码行中插入一个断点。

代码示例：
   
    brightness : function() {
        debugger;
        var r = Math.floor(this.red*255);
        var g = Math.floor(this.green*255);
        var b = Math.floor(this.blue*255);
        return (r * 77 + g * 150 + b * 29) >> 8;
    }

![](https://developer.chrome.com/devtools/docs/console-files/debugger.png)


###统计表达式执行次数
`count()`方法用于统计表达式被执行的次数，它接受一个字符串参数用于标记不同的记号。如果两次传入相同的字符串，该方法就会累积计数。

下面的代码示例显示了统计用户登录次数：

    function login(user) {
        console.count("Login called for user " + user);
    }

    users = [ // by last name since we have too many Pauls.
        'Irish',
        'Bakaus',
        'Kinlan'
    ];

    users.forEach(function(element, index, array) {
        login(element);
    });

    login(users[0]);

![](https://developer.chrome.com/devtools/docs/console-files/console-count.png)


## 使用  Command Line API
控制台绝对不仅仅是简单的日志输出。它是一个功能完整的终端页面交互窗口，Command Line API 包含下面的特性：

+ 快捷的DOM元素选择函数
+ 提供检测CPU性能的方法
+ 提供一系列Console API 的别名
+ 事件监控
+ 查看对象事件绑定情况

###计算表达式
控制台会自动计算你输入的所有JavaScript表达式，它还支持命令补全. 当你输入一个对象的时候，其属性会自动提示，你可以使用`↑` 和 `↓` 进行选择。 使用`→`选择当前提示。

![](https://developer.chrome.com/devtools/docs/console-files/evaluate-expressions.png)


###选择元素
选择元素可以使用快捷方式，与传统方式比起来，这大大的节省了时间：arts.

+ `$()` - 返回满足指定CSS规则的第一个元素，此方法为`document.querySelector()`的简化。
+ `$$()` - 返回满足指定CSS规则的所有元素，此方法为`querySelectorAll()`的简化。
+ `$x()` - 返回满足指定XPath的所有元素。

代码示例：
    
    $('code') // Returns the first code element in the document.
    $$('figure') // Returns an array of all figure elements in the document.
    $x('html/body/p') // Returns an array of all paragraphs in the document body.

###审查DOM元素和JavaScript内存对象

`inspect()`接受DOM元素或者js对象引用作为参数。如果传入的是一个DOM元素，则DevTools会自动转到元素面板并显示该元素的结构。如果传入的是一个JS对象引用，则会打开分析器面板。

*下面的代码首先选择页面中的一个元素，并且将其显示在元素面板中。`$_`表示上一个表达式的输出结果*

    $('[data-target="inspecting-dom-elements-example"]')
    inspect($_)


###访问最近选择的元素和对象
控制台会存储最近5个被选择的元素和对象。当你在元素面板选择一个元素或在分析器面板选择一个对象，记录都会存储在栈中。 可以使用`$x`来操作历史栈，x是从0开始计数的，所以`$0`表示最近选择的元素，`$4`表示最后选择的元素。

###监控事件
`monitorEvents()`会输出指定监控目标的事件信息。该方法的第一个参数表示被监控的对象，第二个参数表示要监控的时间，如果不填则会默认返回该对象上所有事件的监控信息。你可以将数组传入第二个参数，来同时监控多个事件。

代码，监听页面的点击事件：

    monitorEvents(document.body, "click");

如果某个事件类型对应了一组标准的JavaScript事件，则指定该类型监听，会对这些事件都生效。[Command Line API](https://developer.chrome.com/devtools/docs/commandline-api#monitoreventsobject-events)包含了事件类型的说明。

要结束事件监控只需要调用`unmonitorEvents()`，将指定对象的监控移除。


###控制CPU分析器
调用`profile()`方法可以开启CPU分析，你可以传入一个字符串参数对分析器进行命名。结束的时候可以直接调用`profileEnd()`。

    profile()
    profileEnd()

![](https://developer.chrome.com/devtools/docs/commandline-api-files/profile-panel.png)

如果你创建了多个名字相同的分析器，则会自动组合在一起：

    profile("init")
    profileEnd("init")
    profile("init")
    profileEnd("init")

![](https://developer.chrome.com/devtools/docs/commandline-api-files/profile-panel-2.png)

多个分析器可以一起执行，而且并不需要按照创建的顺序去关闭。

按照创建顺序关闭
    
    profile("A")
    profile("B")
    profileEnd("A")
    profileEnd("B")

不按照创建顺序关闭

    profile("A")
    profile("B")
    profileEnd("B")
    profileEnd("A")

##设置
在设置-通用中，你可以进行四项设置：

+ 隐藏网络消息 - 隐藏关于网络情况的日志，例如屏蔽404或500的日志。
+ 记录 XMLHttpRequests - 设置是否记录 XMLHttpRequest。
+ 切换页面时保存日志 -在页面切换的时候是否保存日志。
+ 显示时间戳 - 每条语句被调用的时候显示时间戳，开启本功能会关闭 [message stacking](#消息栈).


##总结
Chrome DevTools提供了一个给力的控制台。你现在应该已经了解如何使用它存储信息和分析元素数据。它的功能还在不断的扩展。如果说web是你的花园，那么他们就是你的砖瓦:)