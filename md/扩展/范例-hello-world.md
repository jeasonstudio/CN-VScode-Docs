---
Order: 2
Area: extensions
TOCTitle: Example-Hello World
ContentId: DC915D6C-13D4-4022-9101-57C4A4118B07
PageTitle: Your First Visual Studio Code Extension - Hello World
DateApproved: 5/9/2016
MetaDescription: Create your first Visual Studio extension (plug-in) with a simple Hello Word example.  This walkthrough will take you through the basics of VS Code extensibility.
---

# 实例 - Hello World

## 你的第一个扩展应用

这篇文档将带你创建你的第一个 VS Code 扩展应用（“Hello World”）并解释基本的 VS Code 扩展概念。  

在这个演示中，你将添加一个新命令到 VS Code 中，执行这个命令会显示一个简单的“Hello World”信息。这个演示之后，你将要与 VS Code 进行交互并查询用户当前所选择的文本。

## 前提条件

在你的 `$PATH` 中需要有一个已安装且可用的 [node.js](https://nodejs.org/en/)

## 生成一个新的扩展应用

添加一个自定义的功能到VS Code中的最简单的方式是通过添加一个命令。这个命令注册一个能够通过命令面板或者已绑定的快捷键调用的回调函数。

我们已经编写好一个 Yeoman 生成器来帮助你上手。安装 Yeoman 和 [Yeoman VS Code 扩展应用生成器](/docs/tools/yocode.md)并搭建一个新的扩展应用的脚手架。

```sh
npm install -g yo generator-code
yo code
```

对于这个 hello world 扩展应用，你可以采用 **TypeScript** 编写或者 **JavaScript** 编写。这个例子中，我们选用的是 **TypeScript** 。

![The command generator](images/example-hello-world/generator.png)

## 运行你的扩展应用

* 启动 VS Code，选择 `File` > `Open Folder` 然后选取你之前生成的那个目录。
* 按 `kb(workbench.action.debug.start)` 或者点击 `调试` 图标然后点击 `开始`。
* 一个新的VS Code窗口将会以一个特殊的模式（`扩展开发主机`）打开，并且**这个新窗口现在已经感知到你的扩展应用**。
* 恭喜你！你已经创建并执行了你的第一个 VS Code 命令！

![Running VS Code with an extension](images/example-hello-world/running.png)

## 扩展应用的结构

运行之后，这个已生成的扩展应用应当有以下的结构：

```
.
├── .gitignore
├── .vscode                     // VS Code integration
│   ├── launch.json
│   ├── settings.json
│   └── tasks.json
├── .vscodeignore
├── README.md
├── src                         // sources
│   └── extension.ts			// extension.js, in case of JavaScript extension
├── test                        // tests folder
│   ├── extension.test.ts	   // extension.test.js, in case of JavaScript extension
│   └── index.ts	            // index.js, in case of JavaScript extension
├── node_modules
│   ├── vscode                  // language services
│   └── typescript              // compiler for typescript (TypeScript only)
├── out                         // compilation output (TypeScript only)
│   ├── src
│   |   ├── extension.js
│   |   └── extension.js.map
│   └── test
│       ├── extension.test.js
│       ├── extension.test.js.map
│       ├── index.js
│       └── index.js.map
├── package.json                // extension's manifest
├── tsconfig.json               // jsconfig.json, in case of JavaScript extension
├── typings                     // type definition files
│   ├── node.d.ts               // link to Node.js APIs
│   └── vscode-typings.d.ts     // link to VS Code APIs
└── vsc-extension-quickstart.md // extension development quick start
```

让我们仔细看看所有这些文件的用途并且说明他们是干什么用的：

### 扩展应用清单：`package.json`

* 请阅读 [`package.json` 扩展应用清单参考](/docs/extensionAPI/extension-manifest.md)
* 更多信息参阅[`package.json` contribution要点](/docs/extensionAPI/extension-points.md)
* 每个 VS Code 扩展应用必须有一个描述它和它的功能的 `package.json` 文件
* VS Code 在启动的时候读取这个文件并立即对每个 `contributes` 部分做出反应。

#### TypeScript 扩展应用清单的示例

```json
{
	"name": "myFirstExtension",
	"description": "",
	"version": "0.0.1",
	"publisher": "",
	"engines": {
		"vscode": "^0.10.1"
	},
	"categories": [
		"Other"
	],
	"activationEvents": [
		"onCommand:extension.sayHello"
	],
	"main": "./out/src/extension",
	"contributes": {
		"commands": [{
			"command": "extension.sayHello",
			"title": "Hello World"
		}]
	},
	"scripts": {
		"vscode:prepublish": "node ./node_modules/vscode/bin/compile",
		"compile": "node ./node_modules/vscode/bin/compile -watch -p ./"
	},
	"devDependencies": {
		"typescript": "^1.7.5",
		"vscode": "^0.11.x"
	}
}
```

> **注意：** 如果没有编译的需要，JavaScript 扩展应用不需要 `scripts` 字段。

* 这个特定的 package.json 这样描述一个扩展应用：
 * *contributes* 一个使用 `"Hello world"` 标签调用 `"extension.sayHello"` 命令的命令面板（`kb(workbench.action.showCommands)`）条目，
 * 当这个`"extension.sayHello"` 命令被调用的时候，请求获得加载（*activationEvents*）。
 * 在 `"./out/src/extension.js"` 的文件中有它的 *主* JavaScript 代码。

> **注意：** VS Code **不会**在启动的时候就马上加载扩展应用。扩展应用必须通过 [`activationEvents`](/docs/extensionAPI/activation-events.md) 属性写明在什么情况下他能够被激活（加载）。

### 生成的代码

生成的扩展应用代码是在 `extension.ts` 中（或者要是 JavaScript 扩展应用的话，在 `extension.js`中）。

```javascript
// 'vscode' 模块包含 VS Code 扩展性API
// 导入这个模块并且在你的代码中用 vscode 这个别名来引用它
import * as vscode from 'vscode';

// 当你的扩展应用激活的时候，这个方法会被调用
// 第一次命令被执行的时候，你的扩展会被激活
export function activate(context: vscode.ExtensionContext) {

	// 使用控制台输出诊断信息（console.log）和错误（console.error）
	// 这行代码只会执行一次，就是在你的扩展被激活的时候。
	console.log('Congratulations, your extension "my-first-extension" is now active!');

	// 这个命令已经在 package.json 文件中定义
	// 现在使用 registerCommand 提供命令的具体实现
	// 这个 commandId 参数必须与 package.json 中的 command 字段相一致
	var disposable = vscode.commands.registerCommand('extension.sayHello', () => {
		// 每次当你的命令被执行的时候，这里的代码都将被执行

		// 显示一个消息框给用户
		vscode.window.showInformationMessage('Hello World!');
	});
	
	context.subscriptions.push(disposable);
}
```

* 每个扩展应用都应当从他的主文件中名为 `activate()` 的函数中导出，任何在 `package.json` 文件中被描述的 `activationEvents` VS Code都将只调用一次。
* 如果扩展应用使用了操作系统资源（例如 spawns processes），扩展应用可以从它的主文件中名为 `deactivate()` 的函数中导出清理工作的任务，VS Code将在关闭的时候调用这个函数。
* 这个特定的扩展应用导入 `vscode` API 然后注册一个命令，当命令 `"extension.sayHello"` 被调用的时候，这个函数被调用了。这个命令实现的是在VS Code中显示一个“Hello world”消息。


> **注意：**  `package.json` 的 `contributes` 部分添加一个条目给命令面板。在 extension.ts/.js 中的代码定义了 `"extension.sayHello"` 的实现。

> **注意：** 对于TypeScript扩展应用，生成的 `out/src/extension.js` 文件将在运行时中被加载，并被VS Code执行。

### 其他文件

* `.vscode/launch.json` 定义了在扩展开发模式中启动 VS Code。同时在 `preLaunchTask` 指明在`.vscode/tasks.json` 中定义的运行 TypeScript 编译器的任务。
* `.vscode/settings.json` 默认排除 `out` 目录。你也可以根据你要隐藏的文件类型进行更改。
* [`.vscodeignore`](/docs/tools/vscecli.md#advanced-usage) - 告知打包工具在发布扩展的时候忽略哪些文件。
* `README.md` - README文件为VS Code用户们描述你的扩展。
* `vsc-extension-quickstart.md` - 给你的快速开始向导。
* `test/extension.test.ts` - 你可以把你的扩展的单元测试放在这里，然后进行对VS Code API的测试 (详见 [测试你的扩展应用](/docs/extensions/testing-extensions.md))

## 扩展应用激活

目前为止扩展应用中包含的文件的作用已经阐明了，那么你的扩展是如何被激活的：

* 扩展应用开发实例找到扩展应用并读取它的 `package.json` 文件。
 * 然后当你按 `kb(workbench.action.showCommands)` 的时候:
  * 在命令面板中显示已注册的命令。
  * 在这个列表中，有一个在 `package.json` 中定义的 `"Hello world"` 条目。
 * 当选择了 `"Hello world"` 命令：
  * 调用`"extension.sayHello"` 命令：
   * 创建一个 `"onCommand:extension.sayHello"` 激活事件。
   * 所有扩展应用在他们激活的  `activationEvents` 中监听这个激活事件
    * `./out/src/extension.js` 中的文件在 JavaScript VM 中获得加载。
	* VS Code 寻找一个已导出的 `activate` 函数，并调用它。
	* 注册`"extension.sayHello"` 命令，并且现在他的实现被定义了。
  * 调用`"extension.sayHello"` 命令的实现函数。
  * 命令执行显示“Hello World”消息。

## 调试你的扩展应用

假如在已注册的命令中，设置一个断点，在扩展开发 VS Code 实例中运行 `"Hello world"` 命令。

![Debugging the extension](images/example-hello-world/hitbp.png)

> **注意：** 对于 TypeScript 扩展应用，尽管 VS Code 加载并执行的是 `out/src/extension.js`，但是由于生成了 source map `out/src/extension.js.map` 且 VS Code 的调试器支持 source map ，所以实际上你可以直接调试 TypeScript 的源代码。

> **提示：** 调试控制台将显示所有那些你打印到控制台的信息。

学习更多有关于扩展应用[开发环境](/docs/extensions/debugging-extensions.md)的内容。

## 一个小小的改变

在 `extension.ts` （或者 JavaScript 扩展应用中的 `extension.js`），试着把 `extension.sayHello` 命令的实现替换为显示在编辑器中已选择的字符数。

```javascript
var editor = vscode.window.activeTextEditor;
if (!editor) {
	return; // 没有打开文本编辑器
}

var selection = editor.selection;
var text = editor.document.getText(selection);

// 显示一个消息框给用户
vscode.window.showInformationMessage('Selected characters: ' + text.length);
```

> **技巧：** 一旦你改变了扩展应用的源代码，你需要重启 VS Code 扩展应用开发实例。你在第二个实例中可以用 `kbstyle(Ctrl+R)` （Mac: `kbstyle(Cmd+R)`）或者点击位于你主 VS Code 实例顶部的重启按钮来重启。

![Running the modified extension](images/example-hello-world/selection-length.png)

## 安装你的本地扩展应用

目前你编写的这个扩展应用只是运行在一个特定的 VS Code 实例中，扩展应用开发实例。要想你的扩展可以在所有的 VS Code 实例中运行，你需要把它复制到你的本例扩展应用目录中的一个新目录中。

* Windows: `%USERPROFILE%\.vscode\extensions`
* Mac/Linux: `$HOME/.vscode/extensions`

## 发布你的扩展应用

阅读有关如何[共享一个扩展应用](/docs/tools/vscecli.md).

## 下一步

在这个演示中，我们见识到一个非常简单的扩展应用。更多的详细实例，查看[单词计数实例](/docs/extensions/example-word-count.md)，它将展示如何针对特定语言（Markdown）监听编辑器的文档改变事件。

如果你要阅读更多关于扩展应用的一般 APIs，试试看这些主题：

* [扩展应用 API 概述](/docs/extensionAPI/overview.md) - 学习有关VS Code 扩展性的完整范例。
* [API 模式和原则](/docs/extensions/patterns-and-principles.md) - VS Code 扩展性是基于几个指导性模式和原则。
* [贡献要点](/docs/extensionAPI/extension-points.md) - 有关各种 VS Code 贡献要点细则。
* [激活事件](/docs/extensionAPI/activation-events.md) - VS Code 激活事件参考


## 通用问题

没了


