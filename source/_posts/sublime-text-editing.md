title: 'sublime text 的使用'
date: 2016-07-04 14:52:47
category:[编程]
---

Sublime Text 从发布到更新至版本3 再个人笔记本上一直有安装使用。但是其实对于Sublime的真正提高编辑效率的功能了解太少，以至于当用到Sublime编辑文本时，与普通的文本编辑器使用并无二样，效率低不说，某种意义上也是对Sublime的一种不尊重。特此记录一些常用的实用功能，以便后期查用。

**提示** (Mac下用Command键，对应Win用Ctrl键)

## 基本编辑

`Command + Enter` 在当前行下面新增一行然后跳至改行；`Command + Shift + Enter` 在当前行上面增加一行并跳至该行。

![rvzS9Ok.gif](http://ww4.sinaimg.cn/large/006tNbRwgw1f5hw2k9gh4g30h404n0to.gif)

`Ctrl + ←/→` 进行逐词移动，相应的，`Ctrl + Shift + ←/→` 进行逐词选择。
`Command + ←/→` 移动光标到（当前可视编辑区域行首，行尾。

［swap_line_up］移动当前行，快捷键可以自定义，根据系统和配置不同，可能快捷键不同，我的组合设置为
`Ctrl + Command + ↑/↓` 

复制
行复制为`Shift + Command + D`

删除
行删除为`Ctrl + Shift + K`

## 选择

Sublime Text的一大亮点时支持多重选择 -- 同时选择多个区域，然后同时编辑。

`Command + D` 选择当前光标所在的词并高亮该词锁出现的位置，再次`Command + D` 选择该词出现的下一个位置，再多重选词的过程中，使用`Command + K` 进行跳过，再按`Command + D`，使用`Ctrl + U` 进行回退，使用Esc 退出多重编辑。

多重选词一大常用场景就是进行重命名。

有时需要对一片区域的所有行同时编辑，`Command + Shift + L`可以将当前选择区域打散，然后同时编辑：

![0NHpXFl.gif](http://ww4.sinaimg.cn/large/006tNbRwgw1f5hxlbwrw8g30h405kq6a.gif)

有打散自然就有合并，`Command + J`可以把当前选中区域合并为一行。


## 查找&替换

标准查找和替换
当需要查找文中某个关键词出现的其他位置，只需选中该词（通过`Command+D`）然后`Command+F` 调出查找面板，然后`alt+Enter` 就可以查找到所有的关键词出新啊位置，可以进行多重编辑和替换。

`Command + F` 调出搜索框进行搜索，`Command + alt + F` 调出搜索并替换。

多文件搜索 & 替换
使用`Command + Shift + F` 开启多文件搜索&替换。

## 跳转
Sublime Text提供了强大的跳转功能，我们可以再不同的文件/方法/函数中无缝切换。

跳转到文件
Command + P会列出当前打开的文件（或者是当前文件夹的文件），输入文件名后Enter跳至该文件。(查找使用模糊字符串匹配)，可以通过文件名的前缀、首字母或是某部分进行匹配。

跳转到符号

`Command + R` 会列出当前文件中的符号（例如类名和函数名，但无法深入到变量名）
对于Markdown，`Command + R`会列出其大纲。

跳转到某行
`Ctrl + G` 然后输入行号就可以跳转到指定行：

组合跳转
在`Command + P` 匹配到文件后，可以通过输入一下符号进行更精确的位置跳转

- `@` 符号跳转：@symbol跳转到符号所在位置
- `#` 关键字跳转：#keyword跳转到对应关键字位置
- `:` 行号跳转：:12跳转到对应文件的行号
{
	- `@` 符号跳转：@symbol跳转到符号所在位置
	- `#` 关键字跳转：#keyword跳转到对应关键字位置
	- `:` 行号跳转：:12跳转到对应文件的行号
}
## 格式化
`Command + [` 向左缩进，`Command + ]`向右缩进，`Command + Shift + V` 以当前缩进粘贴代码。

## 括号
 `Ctrl + M` 可以快速的在起始括号和结尾括号间切换,`Ctrl+Shift+M`则可快速选择括号间的内容。