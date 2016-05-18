---
Order: 3
Area: extensions
TOCTitle: Example-Word Count
ContentId: 4D9132DC-CDDB-4E07-B2DD-9A7E168BE384
PageTitle: Visual Studio Code Example - Word Count Extension
DateApproved: 5/9/2016
MetaDescription: The Word Count extension (plug-in) example takes you deeper into the Visual Studio Code extensibility model, showing how to interact with the editor and manage extension and VS Code resources.
---

# 示例 - 单词计数

这篇文档假设你已经阅读过[《你的第一个扩展应用》](/docs/extensions/example-hello-world.md)，那篇文章包括 VS Code 扩展性的基础内容。

单词计数是一个向你展示如何创建一个扩展应用来帮助编写 Markdown 的完整教程。在我们开始所有工作之前，让我们先看一个你将要构建的核心功能的Demo来让你了解你接下来需要做什么。

当`Markdown` 文件无论何时被编辑的时候，都添加一个状态栏消息。这个消息包含当前单词的总数以及当你从一个文件切换到另外一个文件的时候，也能更新这个状态。

![Word Count on Status Bar](images/example-word-count/wordcountevent2.gif)

> **技巧：**有任何问题的话，从[这个 GitHub 仓库](https://github.com/microsoft/vscode-wordcount)获取完成后的样例。


## 概述

这个示例有三个部分来带你了解一组相关的概念

1. [更新状态栏](/docs/extensions/example-word-count.md#update-the-status-bar) - 在 VS Code `状态栏`显示自定义文本
2. [订阅事件](/docs/extensions/example-word-count.md#subscribing-to-events) - 根据编辑器事件来更新`状态栏`
3. [清理扩展应用资源](/docs/extensions/example-word-count.md#disposing-extension-resources) - 诸如事件订阅或UI操作的资源释放

首先确认你已经安装好最新的 VS Code 扩展应用生成器并运行它：

```bash
npm install -g yo generator-code
yo code
```

这将启用扩展应用生成器 - 我们将以 TypeScript `New Extension` 选项的示例为基础。现在，简单的按照下面的图片所示那样填入这些字段（用 'WordCount' 作为扩展应用的名称，发布者填你自己的名字）。

![Yo Code Word Count Example Output](images/example-word-count/yo1.png)

现在你可以在生成器输出的目录下打开 VS Code：

```bash
cd WordCount
code .
```

## 运行这个扩展应用

在我们继续之前，我们可以先按一下 `kb(workbench.action.debug.start)` 来运行这个扩展应用以确保一切都工作正常。正如之前 "Hello World" 演示中你所看到的那样，VS Code 打开了另一个加载了你的扩展应用的窗口（**[扩展开发主机]**窗口）。你应当可以在命令面板（按 `kb(workbench.action.showCommands)`）里找到 "Hello World" 命令然后选中它，你将在窗口的顶部看到一个 "Hello World" 的信息框。

现在你可以确保这个扩展应用可以正常运行了，假如你愿意的话你可以一直开着这个扩展应用开发窗口。要测试你修改后的扩展应用的话，你可以在开发窗口中再按一下 `kb(workbench.action.debug.continue)` 或者按 `kbstyle(Ctrl+R)`（Mac: `kbstyle(Cmd+R)`）来重新加载这个扩展应用开发窗口。

## 更新状态栏

用以下所示的代码替换掉之前生成的 `extension.ts` 文件中的内容。它声明并实例化了一个能够统计单词数并显示在 VS Code 状态栏的 `WordCounter` 类。当调用"Hello Word" 命令的时候将会调用 `updateWordCount` 方法。

```javascript
// 'vscode'模块包含 VS Code 扩展性API
// 在你的代码中导入必须的扩展性类型
import {window, commands, Disposable, ExtensionContext, StatusBarAlignment, StatusBarItem, TextDocument} from 'vscode';

// 当你的扩展应用被激活的时候调用该方法。通过在 package.json 中定义的激活事件来控制激活。
export function activate(context: ExtensionContext) {

    // 使用控制台输出诊断信息（console.log）和错误（console.error）。
    // 这行代码只会执行一次，就是在你的扩展被激活的时候。
    console.log('Congratulations, your extension "WordCount" is now active!');

    // 创建一个新的WordCounter实例
    let wordCounter = new WordCounter();

    var disposable = commands.registerCommand('extension.sayHello', () => {
        wordCounter.updateWordCount();
    });

    // 当扩展应用被停用时，把需要清理的东西添加到一个清理列表
    context.subscriptions.push(wordCounter);
    context.subscriptions.push(disposable);
}

class WordCounter {

    private _statusBarItem: StatusBarItem;

    public updateWordCount() {

        // 如果需要的话就创建一个
        if (!this._statusBarItem) {
            this._statusBarItem = window.createStatusBarItem(StatusBarAlignment.Left);
        }

        // 获取当前的文本编辑器
        let editor = window.activeTextEditor;
        if (!editor) {
            this._statusBarItem.hide();
            return;
        }

         let doc = editor.document;

        // 如果当前文档是 MarkDown 文件才更新状态
        if (doc.languageId === "markdown") {
            let wordCount = this._getWordCount(doc);

            // Update the status bar
            this._statusBarItem.text = wordCount !== 1 ? `${wordCount} Words` : '1 Word';
            this._statusBarItem.show();
        } else { 
            this._statusBarItem.hide();
        }
    }

    public _getWordCount(doc: TextDocument): number {

        let docContent = doc.getText();

        // 解析出多余的空格以便可以准确的分离单词
        docContent = docContent.replace(/(< ([^>]+)<)/g, '').replace(/\s+/g, ' ');
        docContent = docContent.replace(/^\s\s*/, '').replace(/\s\s*$/, '');
        let wordCount = 0;
        if (docContent != "") {
            wordCount = docContent.split(" ").length;
        }

        return wordCount;
    }

    dispose() {
        this._statusBarItem.dispose();
    }
}
```

现在让我们试试更新这个扩展应用

因为我们已经设置了监视(在扩展应用的 .vscode\tasks.json 文件中)，所以不需要重新编译，我们就已经有编译好的TypeScript文件了。在你代码运行的那个**[扩展开发主机]** 窗口中只要敲击 `kbstyle(Ctrl+R)`，这个扩展应用就会重新加载（你也可以在你的主开发窗口按 `kb(workbench.action.debug.start)`）。我们依然需要像之前那样用“Hello World”命令来调用。假如你在 Markdown 文件中的话，你的状态栏将会显示单词总数。

![Working Word Count](images/example-word-count/wordcount2.png)

这是个不错的开始，不过如果在文档变化的时候可以自动更新计数的话就更酷了。

## 订阅事件

让我们给你的辅助类加上一组事件。

* `onDidChangeTextEditorSelection` - 如果光标位置改变的时候触发这个事件
* `onDidChangeActiveTextEditor` - 如果活动的编辑器改变的时候触发这个事件

为了做到这点，我们将新增一个类到 `extension.ts` 文件中。它将设置订阅这些事件并请求 `WordCounter` 更新单词计数。同时注意这个类如何作为Disposables来管理这个订阅，以及当它被清理的时候如何停止监听的。

把以下所示的 `WordCounterController` 类添加到 `extension.ts` 文件的末尾。

```javascript
class WordCounterController {

    private _wordCounter: WordCounter;
    private _disposable: Disposable;

    constructor(wordCounter: WordCounter) {
        this._wordCounter = wordCounter;
        this._wordCounter.updateWordCount();

        // 订阅选择集变化事件和编辑器激活事件
        let subscriptions: Disposable[] = [];
        window.onDidChangeTextEditorSelection(this._onEvent, this, subscriptions);
        window.onDidChangeActiveTextEditor(this._onEvent, this, subscriptions);

        // 更新当前文件的计数器
        this._wordCounter.updateWordCount();

        // 将所有的事件订阅放入一个清理容器中
        this._disposable = Disposable.from(...subscriptions);
    }

    dispose() {
        this._disposable.dispose();
    }

    private _onEvent() {
        this._wordCounter.updateWordCount();
    }
}
```

我们不用再调用命令来加载这个单词计数扩展应用，取而代之的是每个 *Markdown* 文件都可以用。

首先，用这个来替换掉 `activate` 函数的主体。

```javascript
// 使用控制台输出诊断信息（console.log）和错误（console.error）。
// 这行代码只会执行一次，就是在你的扩展被激活的时候。
console.log('Congratulations, your extension "WordCount" is now active!');

// 创建一个新的WordCounter类
let wordCounter = new WordCounter();
let controller = new WordCounterController(wordCounter);

// 当扩展应用被停用时，把需要清理的东西添加到一个清理列表
context.subscriptions.push(controller);
context.subscriptions.push(wordCounter);
```

然后，我们必须确保打开一个 `Markdown` 文件的同时激活这个扩展应用。为了做到这点，我们需要修改 `package.json` 文件。我们不再需要通过 `extension.sayHello` 这个命令来激活扩展应用，这个扩展应用预先就已经激活了，所以我们可以从 `package.json` 中删除全部的 `contributes` 属性。

```json
    "contributes": {
        "commands":
            [{
                "command": "extension.sayHello",
                "title": "Hello World"
            }
        ]
    },
```

现在更改你的扩展应用，以便他可以在打开一个 *Markdown* 文件的同时被激活，更新 `activationEvents` 属性为这个：

```json
    "activationEvents": [
        "onLanguage:markdown"
    ]
```

[`onLanguage:${language}`](/docs/extensionAPI/activation-events.md#activationeventsonlanguage)事件的language标识符设置为"markdown"，这样子任何时候打开那种语言的文件都会触发这个事件。

按 `kbstyle(Ctrl+R)` 或 `kb(workbench.action.debug.start)` 重新加载一个窗口来运行这个扩展应用，然后开始编辑一个 Markdown 文件。现在你应该有一个自动更新的单词计数功能。

![Word Count Updating on Events](images/example-word-count/wordcountevent2.gif)

如果你在 `activate` 函数那里设置一个调试断点的话，你会发现它只有在第一个 Markdown 文件被打开的时候被调用了一次。`WordCountController` 构造函数运行并订阅了编辑器事件，所以当打开 Markdown 文件以及它们的文本有变化的时候 `updateWordCount` 就会被调用。

## 自定义状态栏

我们已经见识过如何在状态栏显示一个格式化的文本。VS Code 还允许你进一步的通过颜色，图标，工具提示等等方式自定义你的状态栏。

![vscode-d-ts file](images/example-word-count/vscode-d-ts.png)

如下替换StatusBarItem的更新代码：

```javascript
    // 更新状态栏
    this._statusBarItem.text = wordCount !== 1 ? `$(pencil) ${wordCount} Words` : '$(pencil) 1 Word';
    this._statusBarItem.show();
```

在单词计数的计算值的左边显示了一个 [GitHub Octicon](https://octicons.github.com) `pencil` 图标。

![Word Count with pencil icon](images/example-word-count/wordcount-pencil.png)

## 清理扩展应用资源

现在我们来更深入的探究扩展应用如何通过 [Disposables](/docs/extensions/patterns-and-principles.md#disposables) 来使用 VS Code 资源的。

当一个扩展应用被激活的时候，传递给它一个拥有 `subscriptions` `Disposables` 集合的 `ExtensionContext` 对象。扩展应用能够添加他们的 `Disposable` 对象到这个集合中，并且当扩展应用停用的时候 VS Code 将清理这些对象。

许多创建工作空间或UI对象（例如：`registerCommand`）的 VS Code APIs 会返回一个 `Disposable` ，然后扩展应用能够直接通过调用他们的 `dispose()` 方法来从 VS Code 中移除这些对象。

事件是另一个例如有 `onDid*` 事件订阅者方法返回的一个 `Disposable`。扩展应用通过清理事件的 `Disposable` 来退订一个事件。在我们的示例中，`WordCountController` 通过保存一个自有的在停用时清理的 `Disposable` 集合来操作事件订阅 `Disposables`。

```javascript
    // 订阅选择集变化事件和编辑器激活事件
    let subscriptions: Disposable[] = [];
    window.onDidChangeTextEditorSelection(this._onEvent, this, subscriptions);
    window.onDidChangeActiveTextEditor(this._onEvent, this, subscriptions);

    //将所有的事件订阅放入一个清理容器中
    this._disposable = Disposable.from(...subscriptions);
```

## 本地安装你的扩展应用

到目前为止，你编写的扩展应用都只运行在一个特定的 VS Code 实例（扩展开发主机实例）中。复制这个扩展应用文件夹的内容到[你的 `.vscode/extensions` 目录](/docs/extensions/install-extension.md#your-extensions-folder)下的一个新文件夹中，让你的扩展应用在所有 VS Code 实例中都可用。

## 发布你的扩展应用

阅读关于如何[共享一个应用](/docs/tools/vscecli.md)。

## 下一步

继续阅读以了解有关：

* [Yo Code](/docs/tools/yocode.md) - 学习有关Yo Code的其他选项
* [扩展应用 API](/docs/extensionAPI/overview.md) - 获取扩展应用API的概述
* [自定义](/docs/customization/overview.md) - 主题，设置和快捷键绑定
* [发布工具](/docs/tools/vscecli.md) - 学习如何向公共市场发布一个扩展应用
* [编辑器 API](/docs/extensionAPI/vscode-api.md#window) - 学习更多有关文本文档，文本编辑器和编辑文本的内容

## 通用问题

没了


