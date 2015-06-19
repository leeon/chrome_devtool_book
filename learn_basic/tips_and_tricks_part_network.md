#建议和技巧——Network&Setting篇

##重发异步请求
Network面板中会列出页面中所有的异步请求，在任何一条GET或POST请求上右键选择 “Replay XHR”可以重新发送对应的异步请求.

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_74.png)

##清空网络缓存或cookies
在Network面板中右键，选择 “Clear Browser Cache/Network Cache”。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_75.png)


##记录轨迹 & 导出瀑布流

+ 点击 "record" 开始记录多页面请求
+ 导出请求数据: 右键选择 "Copy Entry as HAR"
+ 导出整个瀑布流: 右键, "Copy All as HAR"

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_76.png)

[扩展阅读：等等，DevTools还能做这个？| Igvita.com](http://www.google.com/url?q=http%3A%2F%2Fwww.igvita.com%2Fslides%2F2012%2Fdevtools-tips-and-tricks%2F%231&sa=D&sntz=1&usg=AFQjCNHwM1MWYUas6E9zsZxBARF0igWUow)


##使用大视图查看更多网络细节

点击Network面板下方的 “Use large resource rows” 可以开启大的视图来查看更多网络请求信息。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_77.png)

小视图：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_78.png)

大视图：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_79.png)


##获取更多信息的技巧
在Network面板中 Timeline一列，单击标题可以在切换不同的数据视角：

+ Timeline（时间线）
+ Start Time（开始时间）
+ Response Time（响应时间）
+ End Time（结束时间）
+ Duration（耗时）
+ Latency（延迟）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/network-left.png)

查看灰色背景的文本，了解下面的信息：

+ 每个请求的HTTP头是什么？
+ 每个请求的首字节响应时间是多少？
+ 哪个资源响应时间最慢?
+ 哪个资源耗时最久？

在每一列的标题栏右键，可以选择是否显示该列，其中有三个是默认不显示的：

+ Cookies
+ Domain
+ Set-Cookies

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/network-right.png)


##WebSocket审查

在Network 面板, 你可以在窗口底部的过滤器选择审查 WebSocket 报文。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/websocketbar.png)

例如，打开 [Echo](http://www.websocket.org/echo.html) demo，在Network面板底部选择"WebSockets"，点击"Connect"按钮。任何通过点击"Send"按钮发送的消息都可以在"Frames"子面板中检测到。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/websocketdemo.png)

绿色的部分表示你的客户端发送的消息。WebSocket审查中既可以审查WebSockeyt握手，也可以看到独立的WebSocket数据帧。

[扩展阅读：等等，DevTools还能做这个？](http://www.igvita.com/slides/2012/devtools-tips-and-tricks/#1)

[扩展阅读：使用DevTools审查WebSocket](http://blog.kaazing.com/2012/05/09/inspecting-websocket-traffic-with-chrome-developer-tools/)


##查找过滤异步请求
在Network面板中，你经常需要用键盘上下寻找特定请求。这时可以通过快捷键 `Ctrl` + `F` 或者 `Cmd` + `F`。

在输入框里，输入想要匹配文件名或url的关键字，结果就会被高亮出来。你可以使用上下箭头在结果间进行切换。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_82.png)

选中 “Filter” 可以只显示那些匹配到的请求，这样可以排除多余信息的干扰。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_83.png)

[扩展阅读：计算网络性能](https://developer.chrome.com/devtools/docs/network.md)

##获取网络栈内部状态数据
"about:net-internals" 页面是一个特殊的URL，在该页面中可以收集网络栈内部状态数据。这些数据可以用来处理网络性能和连接问题，包括了请求性能信息，代理设置和DNS缓存。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_84.png)

注意，`about:net-internals/#tests`也支持指定URL的测试。

**关于Network更加详细的内容，请参考[评估网络性能](https://developer.chrome.com/devtools/docs/network)**


#设置

##模拟触摸事件
触摸这种输入方式在桌面上很难测试，因为大部分桌面系统都不支持触摸。然而在移动端测试又会导致开发周期变长，因为每次变更都需要将修改推送到服务端，然后再到设备上看效果。

解决的方案是在开发机上模拟触摸时间。Chrome DevTools支持单点触控，来使得调试移动应用更加容易。

要支持触摸模拟：

+ 打开 overrides 设置选项卡
+ 勾选 “Enable touch events”

（译注：新版本调整了设备模拟选项，在任一面板，按Esc键调起控制台，让后选择Emulation选项）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_85.png)

现在你可以在代码中设置断点，通过标准的桌面事件来调试触摸事件了。

[扩展阅读：DevTools设备模式](https://developer.chrome.com/devtools/docs/device-mode)

##模拟设备UA以及视图

在开发移动页面时，通常我们会现在桌面上制作原型，然后去处理那些需要在移动设备上特殊显示的部分。现在通过设备的模拟，工作就可以变得更加简单了。

DevTools设备模拟支持不同设备类型和屏幕尺寸。（译注：新版本的Chrome可以直接点击 手机 图标，更加简单的模拟设备型号、屏幕尺寸以及网络）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_86.png)

现在你可以模拟在 Galaxy Nexus 和iPhone这样的设备上进行测试了。

[扩展阅读：DevTools设备模式](https://developer.chrome.com/devtools/docs/device-mode)

##模拟地理位置

在调试使用HTML5 geolocation的应用时，常常需要模拟不同的经度和纬度的输入。

DevTools可以模拟`navigator.geolocation`的数值，也可以模拟位置不可用的情形。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_87.png)

覆盖地理位置：

+ 打开[Geolocation](http://html5demos.com/geo) demo
+ 允许页面使用地理位置
+ 打开设置菜单中的 overrides部分（译注：新的位置在控制台窗口中，通过Esc打开）
+ 勾选“Override Geolocation” 然后输入 Lat = 41.4949819 and Lat = -0.1461206

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_88.png)

刷新页面后，demo会使用你输入的新的地理位置。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_89.png)

1.再勾选“Emulate position unavailable” 选项
2.刷新页面，demo会通知你寻找你的位置失败了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_90.png)

[扩展阅读：DevTools设备模拟](https://developer.chrome.com/devtools/docs/device-mode.html)

##使用Dock-to-right模式调试视图
Dock-to-right 模式在调试小屏幕页面时非常有用:

+ 长按布局切换按钮
+ 左右分栏后，可以拖拽分栏位置来调整视图的宽度。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_92.png)

##禁用JavaScript
进入 Settings -> General 勾选 “Disable JavaScript”可以禁用JavaScript。当DevTools打开并且该选项被选中，当前页面的JavaScript就会被禁用。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/disablejavascript.png)


#常用
##快速在tab间切换
使用 `Cmd` + `]` 和 `Cmd` + `[` (或 `Ctrl` + `]` 和 `Ctrl` + `[`) 可以快速的在DevTools中不同的面板之间进行切换，省时省力。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_94.png)

##获得更好的左右分栏体验
新版本的Chrome在左右分栏的时候，会对DevTools窗口进行上下的拆分，便于查看信息。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_95.png)

当然，如果你的屏幕很宽，直接在设置中取消勾选“Split panels vertically when docked to right”就可以了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/toolbaricons.png)

[扩展阅读：3步获取更好的分栏界面](https://plus.google.com/u/0/115133653231679625609/posts/8bfFX8BVzTQ)


##禁用Cache
在设置界面, 你可以勾选‘Disable cache’ 从而禁用Cache.这在调试的过程中太有用了，但是要注意只有在DevTools打开状态下才会有效的。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/disablecache.png)


##审查 Shadow DOM
拥有Shadow DOM 的元素会在Elements面板中显示

+ 在设置中勾选 ‘Show Shadow DOM’
+ 重启 DevTools

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_98.png)

你可以查看 Shadow DOM了，例如 html5 Rocks这个 [Title](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/)

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_99.png)


##预览所有可调式页面
如果你经常使用远程调试，你可以在地址栏打开“about:inspect”，这样可以看到所有可调试的标签页或者扩展程序。点击'inspect'可以打开对应的页面并启动DevTools。
![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_100.png)

##查看哪些站点有应用缓存
在地址栏访问“about:appcache-internals”，可以查看站点的应用缓存信息。你可以查看哪些站点有缓存，这些站点的修改时间以及所占的空间大小，也可以在该页面中移除某些站点缓存。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_101.png)

##Network/Console 面板多过滤器
在Network面板和Console面板中有多个过滤器供你根据不同的数据维度进行选择。

其实按住 `Cmd`或`Ctrl` 并单击鼠标可以同时选择多个过滤器。效果如下图所示：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_102.png)

##清空缓存并执行硬性重新加载
如果你需要执行页面硬性重新加载，在DevTools开启的状态下，长按浏览器刷新按钮。接下来可以看到一个下拉菜单，在菜单里可以同时执行清空缓存并重新加载。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_104.png)


##使用Chrome任务管理器
Chrome任务管理器允许你查看GPU，CPU，JavaScript内存使用，CSS和脚本缓存等信息。

执行下面的操作打开任务管理器:

1. 单击Chrome工具栏中的菜单按钮
2. 选择工具
3. 选择任务管理器
4. 在这里你可以通过在某列鼠标右键查看任何一个进程附加信息或者结束一个进程。
