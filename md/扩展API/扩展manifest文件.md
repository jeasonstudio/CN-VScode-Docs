---
Order: 2
Area: extensionapi
TOCTitle: Extension Manifest
ContentId: C4F184A5-A804-4B0B-9EBA-AFE83B88EE49
PageTitle: Visual Studio Code Extension Manifest File - package.json
DateApproved: 4/14/2016
MetaDescription: At the core of Visual Studio Code's extensibility model is an extension (plug-in) manifest file where your extension declares its extension type(s), activation rules and runtime resources.
---

# 扩展清单文件 - package.json

每个VS Code扩展需要一个清单文件`package.json`，该文件位于扩展的根目录中。


## 字段

名称 | 是否必要 | 类型 | 说明
---- |:--------:| ---- | -------
`name` | 是 | `string` | 扩展的名称，该名称必须为小写且不能有空格。
`version` | 是 | `string` | [SemVer](http://semver.org/) 兼容版本.
`publisher` | 是 | `string` | [发布人名字](/docs/tools/vscecli.md#publishers-and-personal-access-tokens)
`engines` | 是 | `object` | 一个至少包含`vscode`键值对的对象，该键表示的是本扩展可兼容的VS Code的版本，其值不能为`*`。比如 `^0.10.5` 表示扩展兼容VS Code的最低版本是`0.10.5`。
`license` | 否 | `string` | 参考 [npm's 文档](https://docs.npmjs.com/files/package.json#license). 如果你确实需要在扩展根目录下有一个授权文档，那么应该把`license`值设为`"SEE LICENSE IN <filename>"`。
`displayName` | 否 | `string`| 用于在扩展市场中本扩展显示的名字。
`description` | 否 | `string` | 一份简短的说明，用来说明本插件是什么以及做什么
`categories` | 否 | `string[]` | 你希望你的扩展属于哪一类，只允许使用这几种值：`[Languages, Snippets, Linters, Themes, Debuggers, Other]`
`keywords` | 否 | `array` | 一组 **关键字** 或者 **标记**，方便在市场中查找。
`galleryBanner` | 否 | `object` | 帮助格式化市场标题以匹配你的图标，详情如下。
`preview` | 否 | `boolean` | 在市场中把本扩展标记为预览版本。
`main` | 否 | `string` | 扩展的入口点。
[`contributes`](/docs/extensionAPI/extension-points.md) | 否 | `object` | 一个描述扩展 [贡献点](/docs/extensionAPI/extension-points.md)的对象。
[`activationEvents`](/docs/extensionAPI/activation-events.md) | 否 | `array` | 一组用于本扩展的 [激活事件](/docs/extensionAPI/activation-events.md)。
`dependencies` | 否 | `object` | 你的扩展所需的任何运行时的Node.js依赖项，和 [npm's `dependencies`](https://docs.npmjs.com/files/package.json#dependencies)一样。
`devDependencies` | 否 | `object` | 你的扩展所需的任何开发的Node.js依赖项. 和 [npm's `devDependencies`](https://docs.npmjs.com/files/package.json#devdependencies)一样。
`extensionDependencies` | 否 | `array` | 一组本扩展所需的其他扩展的ID值。扩展的ID值始终是 `${publisher}.${name}`。比如：`vscode.csharp`。
`scripts` | 否 | `object` | 和 [npm's `scripts`](https://docs.npmjs.com/misc/scripts)一样，但还有一些[额外VS Code特定字段](/docs/tools/vscecli.md#pre-publish-step).
`icon` | 否 | `string` | 一个128x128像素图标的路径。

也可以查看[npm's `package.json`参考文档](https://docs.npmjs.com/files/package.json).

## 范例

这里有一个完整的`package.json`：

```json
{
	"name": "Spell",
	"displayName": "Spelling and Grammar Checker",
	"description": "Detect mistakes as you type and suggest fixes - great for Markdown.",
	"icon": "images/spellIcon.svg",
	"version": "0.0.19",
	"publisher": "seanmcbreen",
	"galleryBanner": {
		"color": "#0000FF",
		"theme": "dark"
	},
	"license": "SEE LICENSE IN LICENSE.md",
	"bugs": {
		"url": "https://github.com/Microsoft/vscode-spell-check/issues",
		"email": "smcbreen@microsoft.com"
	},
	"homepage": "https://github.com/Microsoft/vscode-spell-check/blob/master/README.md",
	"repository": {
		"type": "git",
		"url": "https://github.com/Microsoft/vscode-spell-check.git"
	},
	"categories": [
		"Linters", "Languages", "Other"
	],
	"engines": {
		"vscode": "0.10.x"
	},
	"main": "./out/extension",
	"activationEvents": [
		"onLanguage:markdown"
	],
	"contributes": {
		"commands": [
			{
				"command": "Spell.suggestFix",
				"title": "Spell Checker Suggestions"
			}
		],
		"keybindings": [
			{
				"command": "Spell.suggestFix",
				"key": "Alt+."
			}
		]
	},
	"scripts": {
		"vscode:prepublish": "node ./node_modules/vscode/bin/compile",
		"compile": "node ./node_modules/vscode/bin/compile -watch -p ./"
	},
	"dependencies": {
		"teacher": "^0.0.1"
	},
	"devDependencies": {
		"vscode": "^0.11.x"
	}
}
```

## 市场呈现要点

为了让你自己的扩展在[VS Code市场]中看起来更好，这里有几个要点和建议。

始终使用最新的`vsce`，即用`npm install -g vsce`可保证最新。

在你的扩展根目录中编写一个`README.md`的MAERKDOWN文档，这样我们会在市场中的扩展信息中显示其中的内容。你可以在`README.md`中提供图片的相对路径链接。

这里有几个例子做说明：

1. [Spell-Checker](https://marketplace.visualstudio.com/items/seanmcbreen.Spell)
2. [MD Tools](https://marketplace.visualstudio.com/items/seanmcbreen.MDTools)


请提供一个良好的显示名称和描述。这对于市场和产品显示都非常重要。在VS Code中这些字符串能用于文本搜索，并且有相关关键字将有很大帮助。
```json
	"displayName": "Spelling and Grammar Checker",
	"description": "Detect mistakes as you type and suggest fixes - great for Markdown.",
```

在市场页面头中，有一个图标以及对比色横幅也会让扩展看起来非常棒，`theme`属性指的是在横幅中使用的字体：`dark`或者是`light`。
```json
	"icon": "images/spellIcon.svg",
	"galleryBanner": {
		"color": "#5c2d91",
		"theme": "dark"
	},
```

你也可以设置一些其他的链接(错误、主页、代码库)，他们会在市场中**资源**一栏所呈现出来。
```json
	"license": "SEE LICENSE IN LICENSE.md",
	"bugs": {
		"url": "https://github.com/Microsoft/vscode-spell-check/issues"
	},
	"homepage": "https://github.com/Microsoft/vscode-spell-check/blob/master/README.md",
	"repository": {
		"type": "git",
		"url": "https://github.com/Microsoft/vscode-spell-check.git"
	}
```

市场资源链接 | package.json 属性
-----------------|-----------------------
支持 | `bugs:url`
开始页 | `repository:url`
主页 | `homepage`
授权 | `license`

为你的扩展设置`category`。在市场中，同一个`category`将会放在一起，这样就方便过滤和查找。


>**注意** 为你的扩展使用正确的值，只能使用这些值`[Languages, Snippets, Linters, Themes, Debuggers, Other]`

```json
	"categories": [
		"Linters", "Languages", "Other"
	],
```

## 结合扩展贡献

`yo code`生成器能让你轻松打包文本主题、颜色设置和代码片段并创建新的扩展。当生成器运行时，它为每个选项创建一个完整的独立扩展包。然而很多时候我们更倾向于创建一个包含多个贡献点的扩展。比如说，如果你希望为一门新语言添加支持，则希望为用户提供带有代码着色的语言定义和代码段功能，甚至可以提供调试支持。


要使能够结合扩展贡献，仅仅只需要编辑已经存在的清单文件`package.json`并添加新的贡献点和关联文件即可。

以下是一个扩展的清单文件，它包含了Latex语言定义(语言标识符和文件扩展名)、着色器（`grammar`)和代码段。

```json
{
	"name": "language-latex",
	"description": "LaTex Language Support",
	"version": "0.0.1",
	"publisher": "someone",
	"engines": {
		"vscode": "0.10.x"
	},
	"categories": [
		"Languages",
		"Snippets"
	],
	"contributes": {
		"languages": [{
			"id": "latex",
			"aliases": ["LaTeX", "latex"],
			"extensions": [".tex"]
		}],
		"grammars": [{
			"language": "latex",
			"scopeName": "text.tex.latex",
			"path": "./syntaxes/latex.tmLanguage"
		}],
		"snippets": [{
			"language": "latex",
			"path": "./snippets/snippets.json"
		}]
	}
}
```

注意，扩展的清单文件中`categories`属性现在可以同时包含`Languages`和`Snippets`，这样方便在市场中查找和过滤。

>**要点** 确保你的多个贡献点使用的是相同的标识符。在上例中，三个贡献点都是使用“latex”作为语言标识符。这让VS Code知道语法着色器和代码段是用于LaTeX语言并当编辑LaTex文件时激活它。

## 下一步
要想了解更多关于VS Code可扩展性模型， 可以查看这些主题：

* [贡献点](/docs/extensionAPI/extension-points.md) - VS Code 贡献点参考文档
* [激活事件](/docs/extensionAPI/activation-events.md) - VS Code 激活事件文档
* [扩展市场](/docs/editor/extension-gallery.md) - 了解更多的VS Code扩展市场

## 常见问题

暂无
