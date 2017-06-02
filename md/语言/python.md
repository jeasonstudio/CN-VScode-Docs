---
Order: 9
Area: languages
TOCTitle: Python
ContentId: c2cb770d-571d-4edf-9eb9-b5b8977c21a0
PageTitle: Python with Visual Studio Code
DateApproved: 5/4/2017
MetaDescription: Learn about Visual Studio Code editor features (code completion, debugging, snippets, linting) for Python.
---
# VS Code 对 Python 的支持

VS Code 通过[扩展](/md/编辑器/扩展市场.md)对 Python 充分支持。[市场](https://marketplace.visualstudio.com)中流行的扩展对代码补全、linting、调试、代码格式化、代码片段等等提供了支持。

> [下载 VS Code](https://code.visualstudio.com/download) - 如果您还未下载 VS Code，那就快为您的平台（Windows，Mac，Linux）安装一个吧。

## 安装 Python 扩展

VS Code 是一个只包含基本特性的轻量编辑器。通过安装其中一个流行的Python扩展插件，即可让 VS Code 添加对 Python 的语言支持。

1. 选择一个扩展。
2. 在命令面板 `kb(workbench.action.showCommands)` 输入 `ext install` 安装插件。

<div class="marketplace-extensions-python"></div>

> 小贴士: 上示的扩展插件是动态获取的。点击上面的扩展插件名称可阅读描述和评论，判断哪个扩展最适合你。详情见 [市场](https://marketplace.visualstudio.com/vscode).

本文档中的例子将使用 Don Jayamanne 流行的全部特性 [Python 扩展](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python).

## 代码补全

Python 扩展支持代码补全和智能提示。[智能提示](/md/编辑器/intellisense.md) 是一系列特性的通用术语，包括借助你所有文件以及内置或第三方模块进行代码智能补全（上下文方法和变量提示）。

快速查看方法、类名和文档。

<video id="python-code-completion-video" src="https://az754404.vo.msecnd.net/public/python-intellisense.mp4" poster="/images/python_python-intellisense-placeholder.png" autoplay loop controls muted></video>

> 小贴士：按下快捷键 `kb(editor.action.triggerSuggest)` 触发代码补全。

## Linting

Linting 用于分析 Python 代码的潜在错误。使用 VS Code 可以快速导航到代码中错误或警告的部分。

<video id="python-linting-video" src="https://az754404.vo.msecnd.net/public/python-linting.mp4" poster="/images/python_python-linting-placeholder.png" autoplay loop controls muted></video>

> 小贴士： [Don Jayamanne 的 Python 扩展](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python) 为您提供了三种不同的linter选择 - [Pylint](https://www.pylint.org/), [Pep8](https://pypi.python.org/pypi/pep8), 和 [Flake8](https://flake8.readthedocs.io/en/latest/). 详情见 [wiki](https://github.com/DonJayamanne/pythonVSCode/wiki/Linting) 。

## 调试

告别 “print” 语句调试！您可以设置断点，检阅数据，以及使用调试控制台，来调试不同类型的Python应用程序（包括多线程、web和远程应用程序）。

<video id="python-debugging-video" src="https://az754404.vo.msecnd.net/public/python-debugging.mp4" poster="/images/python_python-debugging-placeholder.png" autoplay loop controls muted></video>

> 小贴士：按照 [wiki](https://github.com/DonJayamanne/pythonVSCode/wiki/Debugging) 给出的指令进行调试，包括设置你的 `launch.json` 调试配置和常见故障排除。

> 小贴士：想了解更多关于 VS Code 的调试信息，可见 [调试文档](/md/编辑器/调试.md)。

## 代码片段

代码片段将把生产力提升到更高一个层次。您可以配置 [自己的代码片段](https://code.visualstudio.com/docs/editor/userdefinedsnippets) 或使用扩展提供的片段。

<video id="python-snippets-video" src="https://az754404.vo.msecnd.net/public/python-snippets.mp4" poster="/images/python_python-snippets-placeholder.png" autoplay loop controls muted></video>

> 小贴士：使用快捷键`kb(editor.action.triggerSuggest)`，代码片段将和代码补全出现在相同的地方。

## 配置

您需要安装 [扩展](/md/语言/python.md#安装-Python-扩展) 和 [Python](https://www.python.org/downloads/)。其他依赖项是可选的，取决于您想使用的特性。在 [扩展 README](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python#requirements) 中了解更多需求。

## 下一阶段

* [安装扩展](/md/编辑器/扩展市场.md) - Python 扩展可在 [市场](https://marketplace.visualstudio.com/vscode) 获得。
* [基础功能](/md/编辑器/基础.md) - 了解更多 VS Code 编辑器的强大功能。
* [代码导航](https://code.visualstudio.com/docs/editor/editingevolved) - 更快捷地找到相应的源代码。

## 常见问题

**Q: 为什么 linting 不能正常运作？**

**A:** 首先，确保您已安装相应的扩展。其次，许多扩展依赖了外部的包，您需要使用 Python 包管理器，比如[pip](https://pypi.python.org/pypi/pip) 或 [easy_install](http://peak.telecommunity.com/DevCenter/EasyInstall)，来安装 [required packages](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python#requirements)。您可以在 [这里](https://github.com/DonJayamanne/pythonVSCode/wiki/Autocomplete-Intellisense) 阅读更多关于 linting 的信息。
