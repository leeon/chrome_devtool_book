#开发工作流

开发者工作流一般包含了几个步骤来实现特定的目标。使用DevTools可以优化你的工作流来节省完成任务的时间，例如定位文件或方法，连续的编辑脚本或样式，保存常用的代码片段，或者简单的重新布局来满足自己的需要。

在本章中，我们将会探索一些列建议来使你的工作流更加的高效。

##将Dock置于右侧进行垂直分屏编辑
你可能发现将DevTools放置于浏览器底部，水平空间大了，但是垂直空间比较小。你可以将DevTools附着在浏览器窗口的右侧，这样你可以在审查左边的页面，在右边进行调试。

右侧的Dock布局可能适用于下面的场景：

+ 你可能在使用一个宽屏显示器，希望最大化的利用空间来审查和调试代码。
+ 你可以将窗口拆分成小于400px的大小(目前Chrome浏览器的最小宽度)来测试布局的尺寸变化。
+ 比较长的脚本在垂直空间里更容易调试

打开一个你希望调试页面的URL，然后通过开关`dock-to-right`和`dock-to-window` 来切换不同布局，或者长按下图中箭头所指示的图标，会显示所有可用的布局选项。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/chrome_docktomain.jpg)

> 注意：DevTools会记住你最后的选择，所以你可以来回的在常用选项之前进行切换。

一旦你选择了某项配置，布局变化会立刻生效。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/chrome_docktoright.jpg)

> 注意: DevTools中每一个tab 都可以拥有自己的自定义布局。这意味着你可以使一个tab中的工具排在右侧，而另一个tab的工具排在窗口底部。

## 搜索，导航和过滤器

### 脚本样式过滤或代码文件名检索
快速定位指定的文件是开发者工作流中不可获取的功能。DevTools支持在所有的脚本、样式表和代码文件中进行检索，使用下面的快捷键：

+ `Ctrl` + `O` (Windows, Linux)
+ `Cmd` + `O` (Mac OS X)

无论当前在哪个面板，都可以随时进行文件的检索。
例如在这个[Todo app](http://todomvc.com/examples/angularjs/#/)中,使用上面的快捷键，界面将会快速的切换到源码面板，并且直接给我们列出所有可查看文件。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_filter.jpg)

从这里，我们可以快速的向下选择特定的文件（例如名字中包含script的文件），进行查看或者编辑。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_basefind.jpg)

> 注意: 我们支持驼峰式书写的检索,例如，要打开FooBarScript.js, 你只需要输入FBaSc就可以了,这可以节约时间。


###在当前文件内搜索

在指定文件内搜索一个特定的字符串，可以通过下面的快捷键：

+ `Ctrl` + `F`(Windows, Linux)
+ `Cmd` + `F` (Mac OS X)

在搜索框输入完关键字后,直接敲回车定位到第一个匹配的结果,继续敲回车可以移动光标到下一个匹配结果。你可以通过上下的方向箭头在搜索结果之间进行移动。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_findone.jpg)

###在当前文件替换文本

除了支持文件内的文本定位之外，DevTools也支持单处和多处文本替换。勾选`Replace`后，窗口会显示第二个输入框来输入要替换内容的新数值。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_find.jpg)


###全局文本搜索

如果你希望在页面加载的所有文件中搜索一段特殊的字符串，你可以使用下面的快捷键进行全局搜索：

+ `Ctrl` + `Shift` + `F` (Windows, Linux)
+ `Cmd` + `Opt` + `F` (Max OS X)

搜索支持大小敏感搜索和正则表达式。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_findall.jpg)

###使用正则表达式搜索
要使用正则表达式进行搜索，只需要在搜索框中输入表达式，勾选`Regular expression`然后敲击回车。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_regex.jpg)

上图的例子中，我们看到如何用正则表达式找到`<div></div>`标签中的匹配内容.

###函数过滤器或者文件内选择器
如果你需要更细的粒度，你可以定位到文件内特定的JavaScript方法或者CSS规则。

打开你选择的页面，然互打开源码面板。你可以使用下面的快捷键打开函数/选择器搜索窗口：

+ `Ctrl` + `Shift` + `O`(Windows, Linux)
+ `Cmd` + `Shift` + `O` (Mac OS X)

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/function_filter.png)
根据你选择的文件类型不同，你将看到相应的JavaScript函数或者CSS声明。直接输入一个函数或声明的名字就可以在下拉列表中看到，选择即可定位到函数或声明的定义的位置。

###跳转到特定行号
DevTools也支持跳转到编辑器的特定行号中。选择一个文件进行编辑，使用下面的快捷键就可以打开跳转的对话框：

+ `Ctrl` + `L` (Windows)
+ `Cmd` + `L`(Mac OS X)
+ `Ctrl` + `G` (Linux)

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_line.jpg)


##实时编辑脚本&样式
DevTools支持动态的实时额编辑样式和脚本而不需要刷新整个页面。这个功能在测试设计的变更和编写脚本原型的时候比较有用。

###脚本
JavaScript代码可以直接在源码面板中进行编辑，要打开一个特定的脚本文件进行编辑：


1. 在元素面板中直接单击脚本的链接（例如`<script src="app.js"></script>`）。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/styles_select.jpg)

2. 或者在源码面板中从目录树中选择文件名。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/styles_sources.jpg)

选择文件后，在面板的右侧会在新的标签页中显示语法高亮的源码文件。

脚本的变更只会在evaluation time被执行，不在页面加载后执行的脚本代码发生变化是不会产生作用的。在后面会被执行的代码产生变化，例如鼠标移动处理函数或者单击回调函数是可以即可看到效果的。

要了解更过关于调试JavaScript代码的信息，可以阅读相关的[文档](https://developer.chrome.com/devtools/docs/javascript-debugging.html)。这里也有一段[录屏](https://www.youtube.com/watch?v=WQZio5DlSXM)来演示实时编辑和断点调试。

>注意: Workspaces 特性已经支持本地文件的编辑，[了解更多](https://developer.chrome.com/devtools/docs/workspaces.html)。


###样式
DevTools也有编辑样式的工作流。打开元素面板，在界面的右侧的一些列子面板中可以看到样式。审查页面的元素时，当前节点的所有属性会被在此处列出来。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/styles_inspect.jpg)


其中"element.style"部分显示了元素中syle属性被预先设置的样式。

接下来的部分是"Matched CSS Rules", 这部分样式是成功匹配CSS选择器条件的样式，对应的样式文件名以及具体的规则行号都会被列出来。匹配成功的选择器会被标为黑色，而没有被匹配的会变灰色。这样不同的选择器就更容易区分了。

在子面板中改变CSS属性，例如border或一个元素的大小，都可以直接在浏览器窗口中看到实时的变化。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/styles_edit.png)

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/styles_hover.png)

回到"Matched CSS Rules" 面板, 点击CSS样式规则旁边的链接，可以直接到源码面板。在这里显示整个的CSS文件，并自动定位到规则所在的行号。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/matched_css.png)

在这里，你可以像在普通编辑器里一样编辑文件，不同的是，这里可以看到实时的编辑效果。


##另存为
一旦你完成了修改，你可以直接将其保存。

在保存文件前，确认已经打开了文件编辑的面板，无论是在源码面板的左侧目录树中打开：

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_select.jpg)

还是通过在"Elements -> Styles "面板中单击文件名:

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/matched.png)

接下来，在左侧目录树对应的文件名或者编辑器里右键选择另存为。在出现的对话框中可以选择覆盖原文件。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_saveas.jpg)

后面保存会默认写在同样的位置。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_save.jpg)


##本地修改
DevTools也会保存本地代码修改的版本历史。如果你已经在Chrome中编辑了脚本或者样式，你可以在文件名右键，选择"Local modifications"来查看修改历史。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_localmodifications.jpg)

*Local modifications* 面板显示的信息包括:

+ 代码修改的差异
+ 修改的时间
+ 被修改文件所属的域

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_history.jpg)

除此之外，点击`revert`链接将会把代码恢复到最初的状态，并移除修改历史。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_changed.jpg)

*Apply original content*可以实现同样的功能，但是有时候你可能需要回退到某个特定的版本，因此有必要维护一个代码修改历史。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/saveas_changed.jpg)

最后"apply revision content"会采用某个特定时间修改的版本。


##定制 JavaScript 代码片段
有时候你可能会希望保存一些小的代码片段、书签和工具以备在浏览器调试代码的时候使用。代码片段是DevTools中的新特性，允许你在源码面板中创建、保存并运行JavaScript代码。该功能目前在[Chrome Canary](https://tools.google.com/dlpage/chromesxs)可用.

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_hero.jpg)

一些代码片段的应用场景包括：

+ 书签 - 你所有的书签都可以存储为代码片段，特别是那些将来希望编辑的。
+ 工具 - 调试页面的工具可以存储起来。目前社区维护的工具[列表](https://github.com/paulirish/devtools-addons/wiki/Snippets)。
+ 调试 - 代码片段提供一个多行支持语法高亮的控制台，使得调试代码更加方便。
+ Monkey-patching code - 代码片段支持你在运行时添加代码,尽管大多数时间里你只需要在源码面板中实时修改代码。

Brian Grinstead 在Github上维护了一个代码片段的项目[bgrins.github.io/devtools-snippets](http://bgrins.github.io/devtools-snippets/).

###开始
要开始使用代码片段，先打开源码面板。如果你还没做其他的操作，其界面应该如下图所示：

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_default.jpg)

点击左上角的布局按钮打开扩展面板。在新窗口中可以看到`Sources`、`Content scripts`和一个新的标签页`Snippets`。点击`Snippets`:

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_expand.jpg)

###创建 Snippets
Snippets 包含两个面板，左侧的为文件目录树，右侧为snippet的具体内容。编辑snippet的体验和在源码面板中操作体验很类似。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_creating.jpg)

在左侧的文件列表中，右键选择`New`可以创建新的snippet。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_new.png)

###Snippet 文件名
Snippet 文件名是自动生成的, 不过你也可以在其创建的时候自定义。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_filename.png)

如果你希望对文件重命名, 直接在文件名上右键`Rename`。选择 `Remove`删除snippet。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_remove.png)

###编辑和执行 Snippets
从左侧文件列表中选择一个 snippet打开，在右侧编辑窗口中可纯编写或粘贴任何JavaScript代码，包括函数和表达式。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_editor.png)

如果一个snippet文件名前面有一个`*`符号，表示这个文件有修改还没有保存。

要运行一个snippet，右键snippet文件名，选择`Run`.也可以单击`Run (>)`按钮。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_run.png)
snippet的输出将会显示在编辑器下方的终端中。

> 注意: 你也可以使用快捷键来运行一段snippet - 只需要选择对应的snippet，然后使用 `Ctrl/Cmd` + `Enter`运行. 这样可以取代运行按钮，这个按钮将会从控制台底部移到调试控制中。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_console.png)
如果你想在终端中执行snippet中的几行，你可以选中目标代码，右键选择`Evaluate in Console`来执行。其快捷键为`Ctrl` + `Shift` + `E`。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_evaluate.png)

代码运行后,表达式的输出结果会显示在编辑器下面的终端窗口中。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_evaluated.png)


###本地修改
如同源码编辑一样，Snippets同样支持查看本地修改历史，并回退到某个历史版本。

在编辑器中右键，选择`Local modifications...`

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_local.png)


###断点调试，观察表达式以及更多
你在源码面板中使用的一些特性，例如添加观察表达式，调试断点，作用域变量，和保存文件在snippet中同样可用。

阅读源码面板的相关的文档来了解这些特性。
![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/sources_breakpoints.jpg)

###保存 Snippets
Snippets 可以直接在浏览器保存以便以后访问，也可以导出到文件系统中。在编辑器中右键可以查看保存选项。


![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippets_contextmenu.png)
保存功能将会持续的覆盖已存在的snippet文件，另存为功能可以将snippet存储为其他位置的新文件。

> 注意: Snippets 存储在 DevTools 的 localStorage.当使用另存为的时候，你可以像存储脚本一样将其存成文件。


###导航 Snippets
与源码面板中的脚本和CSS类似，Snippets 也支持快速的文件定位。

![](https://developer.chrome.com/devtools/docs/authoring-development-workflow/snippet_filter.png)


##资料
+ [Chrome DevTools Revolutions 2013: Workspaces](http://www.html5rocks.com/en/tutorials/developertools/revolutions2013/#toc-workspaces)
+ [My workflow: Never having to leave the DevTools | remy sharp](http://remysharp.com/2012/12/21/my-workflow-never-having-to-leave-devtools/)
+ [The Breakpoint With Addy Osmani And Paul Lewis - Snippets | youtube](http://www.youtube.com/watch?feature=player_detailpage&v=ktwJ-EDiZoU#t=553s)
+ [Chrome Dev Tools: JavaScript and Performance | nettuts](http://net.tutsplus.com/tutorials/tools-and-tips/chrome-dev-tools-javascript-and-performance/)
+ [Iterating with the Chrome DevTools | jeremey kahn](http://www.youtube.com/watch?v=Phw6edMppKg)

