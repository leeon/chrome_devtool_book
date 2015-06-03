#Chrome DevTools 概览

Chrome开发者工具（简称DevTools）是一组网页制作和调试的工具，内嵌于Google Chrome浏览器中。DevTools使开发者更加深入的了解浏览器内部以及他们编写的应用。通过使用DevTools，可以更加高效的定位页面布局问题，设置JavaScript断点并且更好的理解代码优化。

>注意: 如果你是一个web开发者并且希望获取最新版本的DevTools，你可以使用 [Google Chrome Canary](https://tools.google.com/dlpage/chromesxs).


##访问 DevTools
访问DevTools，首先用Chrome打开一个web页面或web 应用，也可以通过下面的方式：

+ 在浏览器窗口的右上方选择Chrome菜单, 然后选择工具 > 开发者工具。
+ 在页面上任意元素上右键，然后选择审查元素。

DevTools窗口会在Chrome浏览器的底部打开。

下面是一些有用的快捷键来快速的打开DevTools:

+ 使用 `Ctrl` + `Shift` + `I` (Mac上为 `Cmd`+`Opt`+`I`)打开DevTools。
+ 使用 `Ctrl` + `Shift` + `J` (Mac上为 `Cmd`+`Opt`+`J`)打开DevTools中的控制台
+ 使用 `Ctrl` + `Shift` + `C` (Mac上为 `Cmd`+`Shift`+`C`)打开DevTools的审查元素模式。

为了日常工作，[学习快捷键](https://developer.chrome.com/devtools/docs/shortcuts)将帮助你节省更多的时间。


##DevTools 窗口
DevTools 在窗口顶部的工具栏对不同的任务功能进行分组。在每个工具栏选项卡和对应的操作面板中，你可以处理某项特殊的任务，例如DOM元素，资源和源码。

![](https://developer.chrome.com/devtools/images/devtools-window.png)

*DevTools现已经支持内置颜色选择器..*

DevTools目前主要包括以下八个主要功能组：

+ Elements
+ Resources
+ Network
+ Sources
+ Timeline
+ Profiles
+ Audits
+ Console

你可以通过 `Ctrl`+`[` 和 `Ctrl`+`]` 快捷键在不同面板之间进行切换。


##审查DOM元素和样式
在Elements面板中你可以通过DOM树的形式查看所有页面元素，并且可以对其进行所见即所得的编辑。
当你需要确认页面某一个HTML片段的时候，可能经常需要使用Element面板，比如，你可能想知道一个图片元素是否拥有id属性以及id的具体值。

![](https://developer.chrome.com/devtools/images/elements-panel.png)

*在DOM中查看一个head元素*

[Read more about inspecting the DOM and styles](https://developer.chrome.com/devtools/docs/dom-and-styles)


##使用Console
[JavaScript 控制台](https://developer.chrome.com/devtools/docs/console)主要为开发者在测试web页面和应用的过程中提供两方面的功能：

+ 在开发过程中，记录代码诊断信息。
+ 作为shell提示窗口用来和页面文档以及DevTools进行交互。

你可以利用Console API提供的方法来记录诊断信息，例如`console.log()`或`console.profile()`。

你可以利用命令行API提供的方法直接在控制台中计算表达式。例如，利用`$()`选择元素或者调用`profile()`来启动CPU性能监控。

![](https://developer.chrome.com/devtools/docs/console-files/expression-evaluation.png)

*在JS 控制台中执行一些命令*

[了解更过关于命令行](https://developer.chrome.com/devtools/docs/console)


##调试 JavaScript
随着JavaScript程序复杂度的增加，开发者需要更加强大的debug工具来快速的发现问题并高效的修复。DevTools包含了一系列有用的工具让调试javaScript变得更加轻松。

![](https://developer.chrome.com/devtools/images/js-debugging.png)

*一个条件断点用于向终端输出日志*

[阅读更多了解如何使用DevTools调试JavaScript代码](https://developer.chrome.com/devtools/docs/javascript-debugging)


##提高网络性能
在网络面板中可以看到网络请求资源的实时信息。明确和定位那些比预期更加耗时的请求是优化web页面的关键步骤。

![](https://developer.chrome.com/devtools/images/network-panel.png)

*上下文目录用于查看网络请求*

[阅读更多了解如何提高网络性能»](https://developer.chrome.com/devtools/docs/network)


##监听
监听面板会在页面加载的时候对其进行分析，然后提供优化和建议来降低页面加载时间，并提提高响应灵敏性。进一步查看，我们推荐使用[PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)。

![](https://developer.chrome.com/devtools/images/audits-panel.png)

*监听给出的建议*


##提高渲染性能
在Timeline面板中，你可以从整体上看到在web页面加载和被使用的过程中时间消耗在哪里了。所有的时间，从加载资源到解析JavaScript,计算样式和重绘都会被标记在时间线上。

![](https://developer.chrome.com/devtools/images/timeline-panel.png)

*标记着不同事件的时间线例子*
[阅读更多了解如何提高渲染性能»](https://developer.chrome.com/devtools/docs/timeline)


##JavaScript & CSS 性能
在分析面板中，你可以分析一个页面或app的执行时间和内存使用情况。该面板帮助你了解资源消耗在哪里，并且帮助你优化代码。目前提供的分析器包括：

+ CPU分析器显示页面JavaScript函数的执行时间。
+ Heap分析器页面JavaScript对象和相关联的DOM节点的内存分布情况。
+ JavaScript分析器显示脚本的执行时间分布。

![](https://developer.chrome.com/devtools/images/profiles-panel.png)

*一个Heap快照*

[阅读更多了解如何提高JavaScript和CSS性能»](https://developer.chrome.com/devtools/docs/profiles)


##审查存储
在资源面板中你可以查看被审查页面的资源情况。你可以对与 HTML5 Database, Local Storage, Cookies, AppCache等进行交互操作。

![](https://developer.chrome.com/devtools/images/resources-panel.png)

*资源面板中显示的[Web Starter Kit](https://developers.google.com/web/starter-kit/)中的JavaScript文件*

[阅读更多了解审查存储资源](https://developer.chrome.com/devtools/docs/resource-panel)


##扩展阅读
DevTools文档中还包括一些其他部分可能对你有所帮助：

+ [Heap 分析](https://developer.chrome.com/devtools/docs/heap-profiling)
+ [CPU 分析](https://developer.chrome.com/devtools/docs/cpu-profiling)
+ [设备模式 & 模拟设备](https://developer.chrome.com/devtools/docs/device-mode)
+ [远程调试](https://developer.chrome.com/devtools/docs/remote-debugging)
+ [DevTools 视频](https://developer.chrome.com/devtools/docs/videos)


##扩展资源

关注[@ChromiumDev](https://twitter.com/ChromiumDev) 或去[论坛](https://groups.google.com/forum/?fromgroups#!forum/google-chrome-developer-tools)提问。


