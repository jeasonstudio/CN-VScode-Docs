---
Order: 12
Area: languages
TOCTitle: Go
ContentId: 6f06908a-6694-4fad-ac1e-fc6d9c5747ca
PageTitle: Go with Visual Studio Code
DateApproved: 2/5/2020
MetaDescription: Learn about Visual Studio Code editor features (code completion, debugging, snippets, linting) for Go.
---
# 在Visual Studio Code中使用Go   
使用Visual Studio Code上的Go扩展，你可以得到[Golang](https://golang.org/)语言特性支持，例如智能提示，代码导航，符号查找，括号匹配，代码片段等。

![go extension banner](images/go/go-extension.png)

你可以从VS Code [Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.Go)安装Go扩展。

## 智能提示   

### 自动补全 

当你编写go文件时，你可以看见带有建议补全的智能提示。这甚至适用于当前，已导入和尚未导入的程序包中的成员。 只需键入任何软件包名称，然后输入`.`，您将获得有关相应软件包成员的建议。

在你的 [settings](/docs/getstarted/settings.md)中设置`go.autocompleteUnimportedPackages` 为 `true`，你将只得到已导入包的建议

>**Tip**: 用 `kb(editor.action.triggerSuggest)` 来手动触发建议.  


### 悬浮信息  

在任何变量，函数或者结构体上悬浮鼠标指针，可以提供对应的信息，例如注释，参数等等。

![Information on hover](images/go/hover.png)
  

默认情况，扩展使用 `godef` 和 `godoc` 获取这些信息。你可以选择使用 `gogetdoc` 代替。设置方法：改变用户设置或工作空间设置中的 `go.docsTool` 。

### 参数帮助

当你调用函数时，打出`(`，一个弹窗为函数提供参数帮助。当你输入一些参数，提示（下划线）移动到下一个参数。

![Signature Help](images/go/signaturehelp.png)

>**Tip**: 当光标在函数调用的`()`之内，用 `kb(editor.action.triggerParameterHints)` 去手动触发参数帮助。

扩展的参数帮助也使用 `godef` 和 `godoc`。你可以选择使用`gogetdoc`代替。设置方法：改变用户设置或工作空间设置中的`go.docsTool`。

## 代码导航  
代码导航特性适用于编辑器中的文本菜单。

- **转到定义** `kb(editor.action.revealDefinition)` - 转到函数定义的源代码
- **peek定义** `kb(editor.action.peekDefinition)` - 打开一个带有类型定义的Peek窗口
- **转到参考** `kb(editor.action.goToReferences)` - 为这个类型显示所有参考


使用 **Command Palette** (`kb(workbench.action.showCommands)`)中的 **Go to Symbol**命令， 你可以通过符号搜索进行导航。

- Go to Symbol in File - `kb(workbench.action.gotoSymbol)`
- Go to Symbol in Workspace - `kb(workbench.action.showAllSymbols)`  

- 转到文件中的符号 - `kb(workbench.action.gotoSymbol)`
- 转到工作区的符号 - `kb(workbench.action.showAllSymbols)` 

You can also navigate back and forth between a Go file and its test implementation using the **Go: Toggle Test File** command.

你还可以在Go文件之间来回导航。它使用 **Go: Toggle Test File** 命令测试执行。

## 构建，提示和检查   Build, lint, and vet

保存时，Go扩展可以在当前文件的包上运行`go build`, `go vet` 和你选择的检查工具（`golint` or `gometalinter`）。通过下面的设置，你可以控制这些特性：

- `go.buildOnSave`
- `go.buildFlags`
- `go.vetOnSave`
- `go.vetFlags`
- `go.lintOnSave`
- `go.lintFlags`
- `go.lintTool`
- `go.testOnSave`


运行上述任何操作所产生的错误和警告将在编辑器中以红色或绿色波浪线显示。这些诊断也在 **问题** 面板中显示（**视图** > **问题**）

## 格式化


你可以用`kb(editor.action.formatDocument)`或者运行**命令面板**（或编辑器中的文本菜单）中的 **格式化文档t** 命令来格式化Go文件。

默认情况下，当你保存Go文件时，会自动格式化代码。你可以设置`editor.formatOnSave` 为 `false` 来禁用自动格式化。也可以通过修改json设置文件去修改

```json
"[go]":  {
        "editor.formatOnSave": false
    }
```

你可以选择三个格式化工具：`gofmt`, `goreturns`, `goimports` 。设置 `go.formatTool` 进行修改。

## 测试

在 **命令面板** 中输入"Go:test",，你可以看到很多测试相关的命令。

![Test Commands](images/go/testcommands.png)

最上边三个可以使用 `gotests` 为当前包、文件、光标所在处中的函数生成测试框架。
最后几个可以使用“go test”在当前包、文件或光标所在处运行测试。还有一个获取测试覆盖率的命令。

## 导入包

执行 **Go: Add Import** 命令，得到你可导入到你的Go文件的包的列表。选择一个，它会被添加到你的Go文件的导入块。

## 重命名符号

用 `kb(editor.action.rename)` 或者运行编辑器文本菜单的**Rename Symbol** 命令可以重命名符号。

## 调试

Go扩展可以让你调试Go代码。你需要先手动安装 [Delve](https://github.com/derekparker/delve) 调试器。通过访问 [Debugging Go code using VS Code](https://github.com/Microsoft/vscode-go/wiki/Debugging-Go-code-using-VS-Code) ，获取设置步骤，远程调试的信息和故障排除指导。

## 下一步

这是一个简短的概述，展示了VSCode中的Go扩展特性。要获取更多信息，看Go扩展[README](https://marketplace.visualstudio.com/items?itemName=ms-vscode.Go)提供的详细介绍。

要获取最新的Go扩展特性或漏洞修复，看[CHANGELOG](https://github.com/Microsoft/vscode-go/blob/master/CHANGELOG.md)。

如果你有任何疑问或者请求开发一个新特性，可以到Go扩展[repo](https://github.com/Microsoft/vscode-go/issues)提出。

如果你想要了解更多VS Code的信息，试试去下边的话题：

* [Basic Editing](/docs/editor/codebasics.md) - A quick introduction to the basics of the VS Code editor.
* [Install an Extension](/docs/editor/extension-gallery.md) - Learn about other extensions are available in the [Marketplace](https://marketplace.visualstudio.com/vscode).
* [Code Navigation](/docs/editor/editingevolved.md) - Move quickly through your source code.
