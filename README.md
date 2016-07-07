
Microsoft Visual Studio Code 中文手册
===============

Visual Studio Code 是微软推出的跨平台编辑器。它采用经典的VS的UI布局，功能强大，扩展性很强。但是  Visual Studio Code 暂时没有中文手册，对于不太熟悉英文的同学会比较吃力。

本项目的初衷是为想使用或者正在使用 Visual Studio Code 的同学提供一个中文手册，方便大家学习使用这个优秀的工具，提高程序开发效率和质量！


## 翻译流程

###第一阶段

先将 [Visual Studio Code Docs](https://code.visualstudio.com/docs) 的内容按现有的目录结构翻译成中文，其中：

- 文章正文内容均放在 `md` 目录下，采用 `md` 格式。
- 文章中所用到的图片资源暂时先放在 `images`目录下,后续图片资源会统一托管到[七牛云存储](http://www.qiniu.com/)
- 图片按照文档的 `主目录-副目录-编号`的格式命名。

####文件命名规则

- 文件名为[Visual Studio Code Docs](https://code.visualstudio.com/docs) 对应文章标题（即下面列出的目录）的`翻译名称（原英文名）`。所有的空格都用 `-` 代替，`注意单词首字母大写。`
- 对于下级子页面文档，将其放在以父级文档名称命名的文件夹下面。

例如：`https://code.visualstudio.com/docs/editor/whyvscode` 这篇文档，对应 `editor` 这个文件夹下的 `WhyVsCode.md` 文件。

###第二阶段

根据翻译文档，制作成类似在线手册或者与官方文档类似的网站，方便大家参阅。

## 参与项目

欢迎你参与翻译本项目，在翻译的过程中，可以锻炼你的英语能力和 Visual Studio Code 的实际应用能力，同时还为他人提供方便，何乐而不为？

一个个 commit 堆积起来就是一个了不起的 repo，欢迎你 Fork 并提交 Pull Request 或者 Issue ，哪怕是改正一个错别字、修正一个病句，我们都会很高兴。

参与方法和步骤如下：

* 登录 https://github.com

* Fork `git@github.com:CN-VScode-Docs/CN-VScode-Docs.git` 或者点仓库地址[CN-VScode-Docs](https://github.com/jeasonstudio/CN-VScode-Docs.git)

* 创建您的特性分支 (git checkout -b new-feature)

* 提交您的改动 (git commit -m 'Added some features or fixed a bug or change a text')

* 将您的改动记录提交到远程 git 仓库 (git push origin new-feature)

* 然后到 github 网站的该 git 远程仓库的 new-feature 分支下发起 Pull Request

如果你有任何疑问或者建议、技巧，欢迎提出Issues，大家一起交流。

## 官方说明文档

* 仓库连接[vscode-docs](https://github.com/Microsoft/vscode-docs.git)

## 正在翻译文章+作者

* OverView+Jeason
* The Basics+Swizard
* Editing Evolved+heshenghuan
* C++ + imbaqian
* Javascript+Styx
* Markdown+Cherry Mill Wong

## 项目翻译目录

* [Overview](https://code.visualstudio.com/docs)

* EDITOR
  * ~~[Setup](https://code.visualstudio.com/docs/editor/setup)~~
  * [The Basics](https://code.visualstudio.com/docs/editor/codebasics)
  * [Extension Marketplace](https://code.visualstudio.com/docs/editor/extension-gallery)
  * [Editing Evolved](https://code.visualstudio.com/docs/editor/editingevolved)
  * [Version Control](https://code.visualstudio.com/docs/editor/versioncontrol)
  * [Debugging](https://code.visualstudio.com/docs/editor/debugging)
  * [Tasks](https://code.visualstudio.com/docs/editor/tasks)
  * [Accessibility](https://code.visualstudio.com/docs/editor/accessibility)
  * [Why Vs Code](https://code.visualstudio.com/docs/editor/whyvscode)

* CUSTOMIZATION
  * [Overview](https://code.visualstudio.com/docs/customization/overview)
  * [User and Workspace Settings](https://code.visualstudio.com/docs/customization/userandworkspace)
  * [Key Bindings](https://code.visualstudio.com/docs/customization/keybindings)
  * [Snippets](https://code.visualstudio.com/docs/customization/userdefinedsnippets)
  * [Colorizer](https://code.visualstudio.com/docs/customization/colorizer)
  * [Themes](https://code.visualstudio.com/docs/customization/themes)
  * [Display Language](https://code.visualstudio.com/docs/customization/locales)

* LANGUAGES
  * [Overview](https://code.visualstudio.com/docs/languages/overview)
  * [JavaScript](https://code.visualstudio.com/docs/languages/javascript)
  * ~~[C#](https://code.visualstudio.com/docs/languages/csharp)~~
  * [C++](https://code.visualstudio.com/docs/languages/cpp)
  * [JSON](https://code.visualstudio.com/docs/languages/json)
  * ~~[HTML](https://code.visualstudio.com/docs/languages/html)~~
  * ~~[PHP](https://code.visualstudio.com/docs/languages/php)~~
  * [Markdown](https://code.visualstudio.com/docs/languages/markdown)
  * ~~[TypeScript](https://code.visualstudio.com/docs/languages/typescript)~~
  * [CSS, Sass and Less](https://code.visualstudio.com/docs/languages/css)
  * [Dockerfile](https://code.visualstudio.com/docs/languages/dockerfile)

* RUNTIMES
  * [Node.js](https://code.visualstudio.com/docs/runtimes/nodejs)
  * [ASP.NET Core](https://code.visualstudio.com/docs/runtimes/ASPnet5)
  * [Unity](https://code.visualstudio.com/docs/runtimes/unity)
  * [Office](https://code.visualstudio.com/docs/runtimes/office)

* EXTENSIONS
  * [Overview](https://code.visualstudio.com/docs/extensions/overview)
  * [Example - Hello World](https://code.visualstudio.com/docs/extensions/example-hello-world)
  * [Example - Word Count](https://code.visualstudio.com/docs/extensions/example-word-count)
  * [Example - Language Server](https://code.visualstudio.com/docs/extensions/example-language-server)
  * [Example - Debuggers](https://code.visualstudio.com/docs/extensions/example-debuggers)
  * [Principles and Patterns](https://code.visualstudio.com/docs/extensions/patterns-and-principles)
  * [Running and Debugging Your Extension](https://code.visualstudio.com/docs/extensions/debugging-extensions)
  * [Installing Extensions](https://code.visualstudio.com/docs/extensions/install-extension)
  * [Testing Extension](https://code.visualstudio.com/docs/extensions/testing-extensions)
  * [Our Approach](https://code.visualstudio.com/docs/extensions/our-approach)

* EXTENSIBILITY REFERENCE
  * [Overview](https://code.visualstudio.com/docs/extensionAPI/overview)
  * [Extension Manifest](https://code.visualstudio.com/docs/extensionAPI/extension-manifest)
  * [Contribution Points](https://code.visualstudio.com/docs/extensionAPI/extension-points)
  * [Activation Events](https://code.visualstudio.com/docs/extensionAPI/activation-events)
  * [API vscode namespace](https://code.visualstudio.com/docs/extensionAPI/vscode-api)
  * [API Complex Commands](https://code.visualstudio.com/docs/extensionAPI/vscode-api-commands)
  * [API Debugging](https://code.visualstudio.com/docs/extensionAPI/api-debugging)

* TOOLS
  * [Publishing Tool](https://code.visualstudio.com/docs/tools/vscecli)
  * [Extension Generator](https://code.visualstudio.com/docs/tools/yocode)
  * [Samples](https://code.visualstudio.com/docs/tools/samples)

（翻译完成的，请使用删除线将对应划去,像下面这样）

    *  ~~[Overview](https://code.visualstudio.com/docs)~~

## 贡献者（按参与时间排序）

- [Jeason](http://jeasonstudio.github.io/)
- [swizard](http://swizardlv.github.io/)
- [heshenghuan](http://heshenghuan.github.io/)
- [Alexi.F](http://alexifeng.com/)
- [jinyutao](https://github.com/jinyutao)
- [yuxuefeng](https://github.com/twem007)
- [chenxinlong](http://github.com/chenxinlong)
- [Cherry Mill Wong](http://http://123.206.79.144/)

（Fork 之后自行添加到最后）
