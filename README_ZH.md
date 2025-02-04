
<h1 align="center">Obsidian Easy Typing</h1>
<div align="center">

![Obsidian Downloads](https://img.shields.io/badge/dynamic/json?logo=obsidian&color=%23483699&label=插件下载量&query=%24%5B%22easy-typing-obsidian%22%5D.downloads&url=https%3A%2F%2Fraw.githubusercontent.com%2Fobsidianmd%2Fobsidian-releases%2Fmaster%2Fcommunity-plugin-stats.json) ![latest download](https://img.shields.io/github/downloads/Yaozhuwa/easy-typing-obsidian/latest/total?style=plastic)

[中文 | [English](https://github.com/Yaozhuwa/easy-typing-obsidian)]

</div>


EasyTyping 是一个 [Obsidian](https://obsidian.md/) 的书写体验增强插件，功能包含编辑时自动格式化文本和符号编辑增强。自动格式化文本对文档的格式进行规范化，并且美化文档的观感。编辑增强优化用户的编辑体验。

**文本自动格式化**提供了首字母大写功能。此外，文本自动格式化可以根据用户设置的规则，在输入过程中对每一行的特定部分自动添加空格，如中文英文间自动添加空格，文本与英文标点间添加空格，文本和行内公式/行内代码/双向链接间自动添加空格，文本区块和用户自定义正则匹配区块间添加空格等。从而对文档的格式进行规范化，并且美化文档的观感。

**文本自动格式化默认在编辑过程中即时生效**，也可以在设置中关闭编辑时自动格式化的选项。也可以通过插件命令（command）来格式化当前文章全文、当前行或者当前选中区域。

**文本编辑增强功能**，比如连续输入两个 `￥` 会变成 `$$`，并将光标定位到中间，输入两个 `【` 会变成 `[[]]`。让中文用户在很多情况下无需切换输入法，在 Obsidian 得到流畅的书写体验！完整的编辑增强功能，包括 1. 符号自动配对/删除；2. 选中文本的符号编辑增强；3. 连续全角符号转半角符号；4. Obsidian 语法相关的编辑增强。**本插件还支持自定义转换规则，具有很高的可玩性。**

注意：本插件专为 Obsidian 中的中英文混合输入设计，对其他语言不一定有效。

# 插件核心功能
## 1. 文本自动格式化
文本自动格式化提供了首字母大写功能。此外，文本自动格式化可以根据用户设置的规则，在输入过程中对每一行的特定部分自动添加空格，如中文英文间自动添加空格，文本与英文标点间添加空格，文本和行内公式/行内代码/双向链接间自动添加空格，文本区块和用户自定义正则匹配区块间添加空格等。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926001743.png)
文本自动格式化的总开关如上，关闭后不会再输入过程中自动格式化文本。但是不会影响符号编辑增强的功能，也不会影响插件的内置命令：格式化全文、格式化当前行/当前选中区域。
### 1.1 首字母大写
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002011.png)
本插件在输入法在英文输入模式下，提供首字母自动大写的功能，即每个句子开头的字母自动大写。设置中可以选择首字母大写仅在输入时生效或者全局生效。**在选择输入时生效的情况下，首字母大写可以撤销，撤销后不会再对该字母进行大写**。

### 1.2 中英文间插入空格/中文间消除空格/标点与文本间插入空格
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002044.png)

文本和标点间自动空格，会智能地在其他文本和英文标点间添加空格。
### 1.3 不同区块间的空格策略
本插件将每个文本行分割成几个区块：文本块、行内公式块、行内代码块、链接块、用户自定义正则匹配块。块与块之间的空格策略可以在设置中改变。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002125.png)

本插件自 5.0 版本后引入了空格策略。一共有三种空格策略可以选择：1. 无要求；2. 软空格；3. 严格空格。默认设置为软空格。

|空格策略|说明|
|:-----|:---:|
|无要求|该区块与其他区块间没有空格要求，即空不空格分割都可以|
|软空格|该区块与其他区块可以由软空格分割，即标点符号也可以作为一种软空格。|
|严格空格|该区块与其他区块间必须有空格分割。|

下面举例进行说明，对于如下文本行：
```markdown
some text,[[markdown link|双向链接]]还有`inline code`。其他文本。
```
插件根据语法分析将其分割成五块：
1. 文本块：some text,
2. 链接块：\[\[markdown link\|双向链接\]\]
3. 文本块：还有
4. 行内代码块：\`inline code\`
5. 文本块：。其他文本

根据默认设置，链接块与其他块之间需要有软空格，其与左边的文本块之间的邻近内容为英文逗号，不符合软空格的要求，所以在文本块 1 与链接块 2 之间添加空格（如果是中文逗号则符合软空格的要求）。

链接块 2 与文本块 3 之间的邻近内容为 `还`，不符合软空格要求，但是由于链接语文本的空格策略设置中选择了**智能空格**，则插件会根据链接块的显示内容（在此处为该链接的别名：双向链接）与右边的文本进行智能空格，则该区块与文本块 3 的两个相邻内容为 `接还`，两个中文间不添加空格，所以最终链接块 2 与文本块 3 之间不添加空格。

文本块 3 与行内代码块 4 之间邻近字符为 `有`，不符合行内代码块空格策略要求的软空格，所以文本块 3 与行内代码块 4 之间添加空格。

行内代码块 4 与文本块 5 之间邻近字符为 `。`，符合行内代码块空格策略要求的软空格，所以行内代码块 4 与文本块 5 之间不添加空格。

最终经过本插件的格式化后的结果为：
```markdown
some text, [[markdown link|双向链接]]还有 `inline code`。其他文本。
```
### 1.4 自定义正则区块
在有些情况下，用户不希望对某特定形式的内容进行格式化，比如 `{}` 内部的内容，或者 `<>` 内部的内容。**本插件可以通过用户自定义正则表达式的方式来让本插件对特定形式的内容不进行格式化**。

此外，每条自定义正则匹配块都可以设置其左右两边的空格策略。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002222.png)

三种空格策略分别用三个符号来表示，不要求空格（-），软空格（=），严格空格（+）。

想要了解正则表达式的使用，可以查看 [《阮一峰：正则表达式简明教程》](https://javascript.ruanyifeng.com/stdlib/regexp.html#)

#### 1.4.1 自定义正则表达式语法
在自定义正则表达式的文本编辑区域，每一行字符串都为一个正则规则，其格式如下：
```
<正则表达式>|<左空格策略><右空格策略>
```
#### 1.4.2 自定义正则表达式规则示例
举例说明，如默认正则表达式区块的第二行内容如下：
```
#[\u4e00-\u9fa5\w\/]+|++
```
首先最后的两个字符串为该正则区块的左右空格策略，这里为++代表左右空格策略都为严格空格。

倒数第三个字符必须为 | ，其用于将正则表达式部分和左右空格策略部分分开，使其视觉上更容易辨认。

剩下的字符串为正则表达式本身，`#[\u4e00-\u9fa5\w\/]+`，该正则表达式可以匹配以 `#` 键开头的后续有一个或者多个符合 `[\u4e00-\u9fa5\w\/]` 范围的字符，该字符包含汉字、字母、数字、下划线以及 / 符号。

这样说起来比较复杂，简单点就是用来识别 Obsidian 中的标签（即 tag）的。

Obsidian 的标签需要在标签左右都添加空格（中文标点符号也不行，必须是空格），否则不会识别为标签。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/input-tag-plugin-off.gif)

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/input-tag-plugin-on.gif)

上面两张 Gif 演示了使用该自定义正则表达式前后，在 Obsidian 输入标签时的不同。

#### 1.4.3 更多自定义正则的应用
比如默认设置中的如下自定义正则规则是用来识别网络链接的
```
(https?://|ftp://|obsidian://|zotero://|www.)[^\s（）《》。,，！？;；：“”‘’\)\(\[\]\{\}']+|++
```
下面的规则是用来识别 Obsidian 的 callout 语法块的。

```
\[\!.*?\][-+]{0,1}|-+
```

`<.*?>|--` 是用来识别双尖括号块的，保证其内部文本不被自动格式化影响。如在使用 Templater 插件创建模板时，需要使用<% tp.file.cursor() %>这样的语法。启用该自定义规则可以防止其内容被错误添加空格（因为内部的点号会被认为句子的结束，从而本插件会自动在点号与后面的文本间添加空格）。

我期待该自定义正则表达式规则可以满足不同用户的个性化需求，它的更多用法也有待大家发掘~~

更多示例见 https://github.com/Yaozhuwa/easy-typing-obsidian/blob/master/UserDefinedRegExp.md 。

## 2 增强编辑
编辑增强包含了 4 个部分的功能，包括 1. 符号自动配对/删除；2. 选中文本的符号编辑增强；3. 连续全角符号转半角符号；4. Obsidian 语法相关的编辑增强。可以在插件设置中分别设置 4 个功能的打开和关闭。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003124.png)
### 2.1 基础编辑增强
基础编辑增强功能提供了一些考虑 Obsidian 及 Markdown 语法的编辑增强。

以下为插件内部所有基础编辑增强的规则，| 代表光标位置
```python
[['··|', '`|`'], ["`·|`", "```|\n```"],
		["【【|】", "[[|]]"], ['【【|', "[[|]]"], ['￥￥|', '$|$'], ['$￥|$', "$$\n|\n$$"], ["$$|$", "$$\n|\n$$"], ['$$|', "$|$"],
		[">》|", ">>|"], ['\n》|', "\n>|"], [" 》|", " >|"], ["\n、|", "\n/|"], [' 、|', " /|"]]
```
- 第一条规则表示 ··| 转化为 \`|\`
- 第二条规则表示 \`·|\` 转化为 \`\`\`\\n|\`\`\`
- 第三和第四条规则为两次【 输入会变成 \[\[|\]\]
- 最后第二条规则表示句首输入、会转化为斜杠符号/。 (为了适配 Obsidian 核心插件 Slash commands)
- 最后一条规则表示空格后面输入、会转化成斜杠符号 /。(为了适配 Obsidian 核心插件 Slash commands)
- 以此类推
### 2.2 符号配对/删除
#### 2.2.1 符号自动配对
符号自动配对即输入成对符号的左半边，插件会自动补全其右半边的内容。

比如：输入《|，会得到《|》（竖线|代表光标位置）。

本插件默认支持的配对符号如下(更多符号的默认配对可使用本插件的自定义转换规则来实现)：
```python
["【】", "（）", "《》", "“”", "‘’", "「」", "『』"]
```
由于英文小括号、中括号、花括号等符号 Obsidian 本体已经提供了自动配对的选项，本插件不重复提供该功能，需要的话只要打开设置选项 `Editor→Auto pair brackets`。
#### 2.2.2 配对符号删除
当光标左右为配对符号时，使用退格键删除时，会自动把整个配对符号删除。

比如：【|】 按退格键，会变成 |。（竖线|代表光标位置）

本插件支持所有上述自动配对的符号的配对删除。此外，插件还提供了公式块、代码块、高亮块符号的快捷配对删除，其规则如下：
```python
[["$|$", "|"], ['```|\n```', '|'], ['==|==', '|'], ['$$\n|\n$$', "|"]]
```

### 2.3 选中文本时的编辑增强
有时我们会想对文中的某些部分转化为双向链接或者是代码块、公式块。在选中文本情况下，我们想输入英文 `$` 符号将选中部分转化为公式块，如果此时是中文输入法，选中的文本将被替换成￥符号。本插件会识别这些场景，并且实现用户心中所想。

|选中的文本|按键输入|最终结果| 
|:-----|:----|:-----|
|文本|【|[文本]|
|x+y|￥|\$x+y\$| 
|some code|·|\`some code\`|

此外，选中文本的情况下输入一些中文配对符号也会对选中的文本左右加上配对符号

|选中的文本|按键输入|最终结果|
|:-----|:-----|:-----|
|文本|《|《文本》| 
|文本|“ 或者 ”|“文本”| 
|文本|‘ 或者 ’|‘文本’|
|文本|<|<文本>|
|文本|（|（文本）| 

### 2.4 连续全角符号转半角
功能如其名称所示，连续输入两个全角符号会转化成半角符号。

插件内置实现的转换规则如下
```python
[["。。|", ".|"], ["！！|", "!|"], ["；；|", ";|"], ["，，|", ",|"],
		["：：|", ":|"], ['？？|', '?|'], ['、、|', '/|'], ['（（|）', "(|)"], ['（（|', '(|)'],
		["》》|", ">|"], ["《《|》", "<|"], ['《《|', "<|"]]
```
如上面第一个规则代表两个连续的中文句号会变成英文的点。第二条规则表示输入两个连续的中文感叹号会变成一个英文叹号，以此类推。

### 2.5 用户自定义编辑转化规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003149.png)

这里参考了 [aptend/typing-transformer-obsidian](https://github.com/aptend/typing-transformer-obsidian) 的转换规则的想法，可以让用户自定义转换规则，从而使插件更通用。感谢 [aptend/typing-transformer-obsidian](https://github.com/aptend/typing-transformer-obsidian)！
#### 2.5.1 选中文本情况下的自定义转换规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003230.png)

在设置栏分别输入触发符号、转换后的左右的字符串，再点击右边的添加规则按钮，即可生成一条用户自定义规则。设置好规则后，在选中文本的情况下，输入设置的触发符号，就会在选中的文本的左右分别添加 `转换后左边字符串` 和 `转换后右边字符串`。

如我分别输入 `-`、`~~`、`~~`，然后添加规则，即可得到如上图中的第一条规则。该规则设置完成后，选中文本，再输入 `-`，则会得到 `~~选中的文本~~`。

已经添加的规则可以点击编辑按钮进行改动，或者删除按钮删除规则。

选中文本自定义转换规则的优先级高于插件内置转换。
#### 2.5.2 删除时的自定义转换规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003212.png)

删除规则需要输入删除前的文本状态和按删除键后的文本状态，用|来表示光标的位置，前后的文本状态都必须有 | 以表明光标位置。光标左右都可以任意添加文本。

如内置的符号配对删除功能其实是添加了一系列删除规则，比如《》的配对删除规则如下

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003249.png)

点击右边加号按钮即可添加规则。同样的每条自定义删除规则也可以进行编辑和删除。

**删除规则只在使用退格键删除光标前文本时生效**，在选中文本或者使用 delete 键向后删除时不会生效。

用户自定义删除规则优先级高于插件内置删除规则。
#### 2.5.3 输入时的自定义转换规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003300.png)

输入时的自定义转换规则类似删除时的自定义转换规则，差别在于其在输入字符的过程中生效。
如上图中我添加了一条自定义转换规则，在我输入 `:)` 时，插件会将其转化为😀。这种转化操作是可以撤销的。

输入时的自定义转换规则优先级比插件内置的转换规则（如符号自动配对、连续全角符号转半角）低。
## 更新记录
更新记录见 [./changelog.md](https://github.com/Yaozhuwa/easy-typing-obsidian/blob/master/changelog.md)

## 致谢
- https://github.com/artisticat1/obsidian-latex-suite
- https://github.com/aptend/typing-transformer-obsidian
## 赞助
如果你喜欢这个插件，并对我表示感谢，你可以在这里请我喝一杯奶茶！

<img src="assets/donate.png" width="400">
