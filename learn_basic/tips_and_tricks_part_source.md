#建议和技巧——代码篇


##调试&DOM编辑

在元素上右键，选择 ‘Break on Subtree Modifications’: 当脚本遍历到该元素子节点并且进行修改操作时，断点调试器就会自动被触发。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_30.png)

同样值得注意的是设置“ Attribute modifications”选项可以在元素的inline style变化时触发调试器，这在调试DOM动画的时候很有用。


##追踪未捕获异常
在 Source 面板，双击 `暂停执行脚本`按钮（`||`）,在未捕获的异常出现时，调试器就会开启，保存调用栈和程序当前的状态信息。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_32.png)


##条件断点
DevTools支持条件断点，我们都知道在代码的行号上单击鼠标可以在当前行设置一个普通断点，程序执行到这里就会暂停。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_33.png)

接着，你可以在断点上右键然后选择 "Edit Breakpoint"，这样就可以看到一个表达式输入框。在里面可以定义条件，如果条件为`True`，断点就会生效。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_34.png)

一个通常的表达式可能是`x === 5`这种，然而在表达式写`console.log`语句也是完全OK的。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_35.png)

这个条件表达式可以正常的工作，并且我们可以很明显看到`console.log`语句在代码经过断点的时候执行了:

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_36.png)

因为`console.log`并没有真正的返回值，所以相当于返回了`undefined`。这样对应的条件断点相当于不满足条件而不会被触发，程序在打印表达式信息后会继续的执行。所以这种做法感觉就相当于硬编码进去一个调试语句而不需要真的修改自己的代码。

[扩展阅读：JavaScript断点调试](http://www.google.com/url?q=http%3A%2F%2Fwww.randomthink.net%2Fblog%2F2012%2F11%2Fbreakpoint-actions-in-javascript%2F&sa=D&sntz=1&usg=AFQjCNE9yz1n3H6Boru1bl11nQdiUwmR4w)


##清晰显示JavaScript代码
一般web页面的代码都是minified压缩的。DevTools支持将代码格式化显示，使代码可读：

+ 前往Source面板选择你想要查看的JavaScript代码
+ 接下来，点击"Pretty print" 按钮 (大概这个样子 `{}`）

你的代码现在看起来一定清晰漂亮多啦！

之前

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_38.png)

之后

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_39.png)


##收藏表达式或者变量值
在调试过程中，你可能需要一遍又一遍的输入相同的变量名或者表达式，有了DevTools你可以将这些常用的变量和表达式添加到`Watch Expression`中。你可以直接对这些内容进行修改，或者只是用于在代码运行的过程中观察这些指的变化。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_40.png)

##查看内部属性
假设你定义了一个变量`s`，它可以进行下面的操作：

    s.substring(1, 4)  // returns 'ell'

`s`一定是一个string类型吗？它也可能是一个包装string对象。在 `watch expressions`添加下面的表达式:

    "hello"
    Object("hello")

第一个是一个普通的字符串，第二个是一个完整的对象。有些让人迷惑的是，二者看起来几乎是一样的，但是后者拥有属性，并且你可以为其添加属性。

展开它的属性列表，你就会发现它并非一个普通对象，它拥有一个内部的属性`[[PrimitiveValue]]`存储着字符串的值。你无法在代码中访问这个属性，但是可以在调试窗口里面看到。

[扩展阅读:通过DevTools学习JavaScript](https://gist.github.com/paulirish/4158604)

##轻松调试 XHRs
在调试窗口中打开“XHR Breakpoints”部分，你可以添加一个URL或者一个字符串来，指定发起某种XMLHttpRequest时开启程序调试。你也可以在任何XHR发起时都进入调试：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_41.jpg)

##检索元素上注册的事件
打开 Elements面板，在DOM树中用鼠标选中一个元素。注意：你也可以在控制台中使用`getEventListeners(targetNode)`选择。

接下来在右侧窗口，展开"Event Listeners"选项。在这里会看到，当前元素所绑定事件列表。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_42.png)

##Esc快速打开控制台
在 Source面板中调试的时候，你有时需要同时访问控制台。这时只需要按`Esc`键，就可以打开控制台。
你可以在控制台中执行JavaScript代码，不过更加给力的地方在于，在代码的调试断点执行JavaScript的环境就是当前暂停的程序上下文。（译注：因此你可以在此时编写代码查看一些特定的数据）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_43.png)

##更加高效的处理断点
当你的程序在调试断点暂停的时候，你可以进行更多的操作：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_44.png)

你或许知道你可以通过 "Continue", "Step Over", "Step Into" 和 "Step Out" 控制程序执行，其实每一项功能都有对应的快捷键。学习这些快捷键操作可以在调代码的过程中更加高效。

Watch Expressions (在窗口的右侧)会实时的现实表达式的值，所以你无须切换到控制台去计算表达式(例如 X === Y)。 

Call Stack (在Watch EXpressions下方)会列出当前系统已经执行函数调用到哪里了。

在 Scope Variables 部分, 你可以在任何函数上右键然后选择 "Jump to definition" 跳转到函数定义的位置。

DOM Breakpoints 会显示那些在 Elements面板被添加调试断点的元素。这个部分将帮助你观察那些事件是否已经成功的绑定到了元素上,以及事件被触发的时候执行了哪些操作。

XHR Breakpoints 的作用在于为XMLHttpReauest请求设置了断点，指定URL可以观察具体的异步请求情况。


##异常时暂停
你可能希望在有异常被抛出的时候暂停JavaScript的执行，然后去检查函数调用栈，作用域变量和app的状态。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_45.png)

点击Scripts面板顶部的黑色暂停按钮可以切换不同的异常处理模式。很可能你并不希望在所有的异常抛出时都去暂停程序，除非你调试的代码都有try/catch语句。

##全文检索
如果你想在所有文件中检索一个字符串，可以使用下面的快捷键：

+ `Ctrl` + `Shift` + `F` (Windows, Linux)
+ `Cmd` + `Opt` + `F`(Max OSX)

检索支持正则表达式和大小写敏感。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_50.png)

##使用DevTools和源码地图调试 CoffeeScript 

源码地图是一种将编译好的成产环境代码还原到开发环境的原始代码的方式，并且是语言无关的。

生产环境中生成的代码一般是被压缩过的，这使得很难定位到生成环境的代码对应到源码中的哪一行。

打开源码地图支持：

+ 打开设置 cog > General
+ 选择 "Enable source maps"

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_51.png)

接下来:

+ 将你的CoffeeScript 转换成 JavaScript，运行: `coffee -c myexample.coffee`
+ 安装 [CoffeeScript Redux](https://github.com/michaelficarra/CoffeeScriptRedux)
+ 创建一个源码地图文件 example.js.map 用来存储所有的代码映射信息: `$ coffee-redux/bin/coffee --source-map -i example.coffee > example.js.map`
+ 确认生成的 JavaScript 文件, example.js, 在文件的末尾有下面的url: `//# sourceMappingURL=example.js.map`

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_52.png)

现在你可以调试CoffeeScript代码了，通过上面的声明语句，DevTools就知道源码在哪里了。

你可以继续使用这个源码地图，在代码压缩的阶段，使用像UglifyJS2的工具来引用该文件，将压缩后的JS代码映射回到CoffeeScript代码而不是JavaScript编译后的输出。


这样你就可以直接调试生产环境的代码然后定位到CoffeeScript源码。

[扩展阅读:Source Maps 101](http://net.tutsplus.com/tutorials/tools-and-tips/source-maps-101/)

**想了解更多关于工作流，请自觉前往[开发工作流](./development_workflow.md)一章。**

