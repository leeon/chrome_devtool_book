#建议和技巧——Profiles篇


##利用`三次快照`发现JavaScript内存泄露

1. 打开DevTools 并切换到 Profiles 面板
2. 执行一个会导致内存泄露的操作
3. 创建一个新的heap快照
4. 重复步骤2和步骤3三次
5. 选择最近的heap快照
6. 下边的默认结果过滤为`All Object`,将其改为`Objects between Snapshot 1 and 2`
7. 这时候你就可以看到一组未被释放的对象，选择其中一个，可以在`Object's retaining tree`中查看什么导致了内存泄露。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_25.png)

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_26.png)

[PPT：排除GMail中的内存泄露](https://docs.google.com/presentation/d/1wUVmf78gG-ra5aOxvTfYdiLkdGaR9OhXRnOlIcEmu2s/pub?start=false&loop=false&delayms=3000&slide=id.g1d65bdf6_0_0)


##了解Heap 分析器中的不同节点含义
红色的节点表示仍然存在的分离DOM树的一部分，并且DOM树种的某个节点仍然在被JavaScript引用（可能是一个闭包或者某些属性）

黄色的节点表示一个分离DOM树的引用，可能是某个对象的属性或者是一个数组元素，在元素和`window`之间可能存在着一条属性链（例如 window.foo.bar[2].baz）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_27.jpg)

[扩展阅读：理解Heap分析器中的节点](https://plus.google.com/u/0/115133653231679625609/posts/hEMupRLRJSF)


##Heap 分析器的其他视图
一个常见的疑惑是，Profile面板中快照结果里的 Comparison, Dominator, Containment 和 Summary 四种视图之间有什么区别。 四个视图分别从不同角度分析快照数据：

Comparison 视图可以显示哪些对象已经被垃圾回收正确释放了。 一般在该视图中比较一次操作前后的内存快照数据。通过检查空闲内存中的变量增量和引用数来确定内存泄露的存在和原因。

Dominators 视图用来确认对象已经没有其他未知的引用，并且垃圾回收可以正常工作。(译注：新版本Chrome中，该面板已经去掉，新增了Statistics，统计不同类型数据所占的内存)

Summary 视图可以按照类型追踪对象及其内存使用情况，对象会以构造器名分组显示，主要用于寻找DOM内存泄露的场景。

Containment 视图可以更清晰的了解到对象的结构，借此可以分析出在全局作用域中对该对象的引用情况(例如window)，可以用来分析闭包，以更低的层次去查看对象情况。


![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_29.png)

[扩展阅读：更加轻松的在Chrome中分析JavaScript内存](http://addyosmani.com/blog/taming-the-unicorn-easing-javascript-memory-profiling-in-devtools/)



**想了解更多关于性能分析的使用技巧，请自觉前往[分析内存性能](https://developer.chrome.com/devtools/docs/heap-profiling)一章。**

