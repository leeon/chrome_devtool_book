#建议和技巧——Elements篇

##使用标尺
在 Settings > General > Show rulers a ruler 中可以开启标尺，当鼠标悬浮在元素上面或者将其选中，标尺就会显示自动显示出来。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_53.png)


##CSS属性自动补全
DevTools支持CSS属性名和值的自动补全（包括带前缀的），在补全列表中你就可以看到当前元素是可以设置哪些属性的。

当你输入属性名或者其值的时候，DevTools会自动给出提示，使用上下箭头可以在提示列表中进行选择。给元素添加属性后，页面就会立刻生效。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_55.png)

在 Styles 面板中，可以选择CSS颜色值，格式包括 名字(例如'red'), HSL, HEX或者RGB。按住`shift`键，在颜色上单击鼠标可以进行不同格式之间的切换。

如果你希望显示一个属性所有支持的值，使用`Ctrl`+`space`。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_56.png)

这个提示列表与具体的属性类型相关（例如font），数字和带前缀的数值也支持。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_57.png)

##颜色选择器
DevTools内置了一个颜色选择器，用鼠标单击颜色的小方块，就会开启选择器。使用选择器可以选择页面中的任何颜色。（译注：这个非常给力，尤其是参考某个页面的时候）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/colorpickercanary.png)

按住`shift`并单击颜色值，可以改变颜色的格式。

##增加 CSS 样式
在一个css规则中大括号中间的任何位置单击鼠标都可以为当前元素添加一个新的CSS属性，添加后属性会立刻生效。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_60.png)

添加完一个属性后，按`tab`键可以继续输入下一个属性。

在Style面板的右侧点击加号按钮，可以添加新的选择器。

注意：其实可以直接编辑选择器，在CSS选择器上单击，就可以直接修改选择器名字，一旦完成修改，之前选择器对应的属性就会应用到新的选择器上。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_62.png)

新的伪类选择器同样使用类似的方式添加。注意，单击右侧的"toggle element states"按钮（加号的旁边），可以开启"Force element state"功能。这个功能非常给力，勾选对应状态，就可以强制的给当前选中的元素加特技（伪类）了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_64.png)

回到 “Matched CSS Rules” 面板, 点击CSS规则旁边的链接，可以直接定位到具体CSS文件的某一行。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_65.png)

##拖拽页面元素
在 Elements 面板里，可以拖拽一个元素来随意调整它的位置。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_66.png)

##强制元素状态
是不是有时希望强行的改变一个元素的状态?

+ 在一个子元素上右键，选择‘审查元素’
+ Elements面板中，在父元素上右键选择"Force Element State"
+ 你可以任意选择`:active`, `:hover`, `:focus`或者 `:visited`

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_67.png)

##编写调试Sass

> 注意: 要在Chrome中调试Sass 需要3.3.0 (pre-release) 以上的 Sass 编译器, 支持source map生成。

处理一个带有预处理CSS的页面比较棘手，以为在DevTools中对CSS样式的修改一般不会更新Sass源码文件。这意味着如果想即时的改变样式，你需要手动的去在其他编辑器中修改源码文件。

最新的Sass工作流中这已经不再是一个问题，如果想支持Sass：

[1] 确认你的DevTools已经开启了实验室功能（译注：在地址栏输入 chrome://flags/ 开启工具实验室功能）

[2] 接着，前往设置页面，选择 Settings cog > Experiments 并勾选 “Sass stylesheet debugging” （译注：最新版本的Chrome已经将该功能移除实验室，可以忽略本步骤）

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/stylesheetdebugging.png)

[3] 前往 General menu > Settings > 勾选 “Enable source maps” 和 “Auto-reload CSS upon Sass save”

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/autoreload.png)

timeout参数可以使用默认值。这取决于Sass编译器多久可以完成编译，你也可以禁用自动加载，而在需要的时候手动去刷新。

[4] 打开你想调试的页面

[5] 接下来，开启Sass编译器，使用如下命令`sass --watch --sourcemap sass/styles.scss:styles.css`，编译器会监测源码文件是否发生变化，并未每个生成的CSS文件创建source map,
如下面的控制台所示：

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_70.png)

*确认Sass调试正确工作* 

[6] 如果正确配置完成，可以在Elements面板看到，每个样式后面对应的链接已经是`.scss`文件以及具体的代码行号了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_71.png)

[7] 点击文件名，就可以直接到Source面板中对应的源码行中，现在就可以直接在DevTools中的语法高亮编辑器中工作了。

![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_72.jpg)

[8] 如果你希望在Source面板中编辑Sass文件，只要确认DevTools能够找到源文件的磁盘位置。在编辑器中右键选择"Save as",可以用现在编辑的文件去覆盖源文件。DevTools支持文件自动加载，这样修改可以在Chrome中立刻生效了。


![](https://developer.chrome.com/devtools/docs/tips-and-tricks/image_73.png)


**想了解更多关于页面元素和样式的使用技巧，请自觉前往[修改DOM样式](https://developer.chrome.com/devtools/docs/dom-and-styles)一章。**
