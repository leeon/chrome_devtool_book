#建议和技巧——Timeline篇

##使用帧模式分析页面
在Timeline面板中，你可以看到web 应用内的耗时分布，例如执行DOM事件、渲染页面布局或者绘制页面元素等。你可以通过：页面帧、事件和实际内存使用三个方面发现程序的问题：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_0.png)

默认情况下 Timeline 不会记录任何数据，你可以通过点击Timeline面板下面的**圆点图标**来开启一个Timeline监控会话。开启Timeline快捷键是`Ctrl` + `E` 或 `Cmd` + `E`。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_1.png)

Timeline开启时，圆点会从灰色变为红色。开启监控后，在页面内执行一些交互操作，然后可以单机按钮停止记录。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_2.png)

网页在浏览器打开的时候，Chrome会生成每一帧将页面渲染在屏幕上。Timeline的帧模式能够帮助你分析每一帧里发生的情况。在帧模式里，阴影部分的竖条对应的是重新计算样式、组合页面等操作所消耗的时间。透明的区域则表示空闲时间，至少在你当前页面是空闲的。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_3.png)

通常，每一帧都是根据刷新频率同步来执行的。在上面例子中，第二帧的耗时稍微超过了15ms,第三帧的任务错过了真正的硬件帧，只能等到下一帧再渲染。因而实际上第二帧消耗的时间加倍了，超过了30ms。

即使你的app中不涉及大量的动画，帧的概念也很重要。因为浏览器要不停的处理一系列输入事件，当你在一个帧里留下了充足的时间来处理这些事件，你的app就能更好的响应，这也意味着更好的用户体验。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_4.png)

一般我们把目标帧频率定在60fps,我们在每帧里最多有16.66ms来处理任务。这个时间并不多，所以尽量的从动画中节省性能消耗是很关键的一种优化方式。

[更多：利用DevTools Timeline 提升程序性能](https://developer.chrome.com/devtools/docs/timeline)



##使用warning找出强制布局事件
在Timeline面板中，如果你看到一个黄色的三角警告符号，这表示你的某些代码会触发强制/同步布局事件。

理想情况下，我们通常避免不必要的布局事件被触发，因为这些事件对页面的性能影响很大。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_5.png)

[更多：Timeline Warnings 嗅探性能](https://plus.google.com/u/0/115133653231679625609/posts/A7rYqkMMmW8)



##分享或分析他人的Timeline
使用Timeline的导入/导出功能，你可以分享自己的Timeline数据或者分析其他人的数据。使用`Ctrl` + `E` 或者 `Cmd` + `E` 记录一段Timeline数据，在Timeline内右键选择`Save Timeline data`可以导出自己的Timeline数据，右键选择`Load Timeline Data`可以导入其他的数据。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_6.png)

##标注Timeline
你可以通过在代码中调用`cnsole.timeStamp()`方法来在Timeline中打上标注。这样更容易找到你自己app中的代码与其他活动代码或浏览器自身实践的关联。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_7.png)

[更多：DevTools Console API - 标注Timeline](./using_console.md#标注-Timeline)

##FPS 计数器/HUD平视显示器
DevTools 提供了一个FPS的监控计数器，用于显示可视化的帧频率。可以在设置-选中`Show FPS meter`来开启。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_8.png)

激活计数器后，你可以在页面的右上角看到一个黑色的区域，里面包含了画面帧的实时数据。有了这个工具，你就可以在实时操作页面的过程中直接看到什么导致了页面帧刷新频率下降，而不用麻烦去打开Timeline。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_9.png)

[更多：使用DevTools 连续绘制模式分析性能|Paul Irish大牛博文](http://updates.html5rocks.com/2013/02/Profiling-Long-Paint-Times-with-DevTools-Continuous-Painting-Mode)

记住只关注FPS计数器可能会让你忽视间歇性的闪烁(译注：frames with intermittent jank，猜测指代的是那些错失物理帧的页面帧)，谨慎的分析这些内容。还要注意的是桌面的FPS并不代表移动设备上的情况，移动设备上的性能分析也十分值得关心。


**想了解更多关于控制台的使用技巧，请自觉前往[Time](https://developer.chrome.com/devtools/docs/timeline)一章。**

