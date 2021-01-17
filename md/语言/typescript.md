---
Order: 9
Area: languages
TOCTitle: TypeScript
ContentId: 05C114DF-4FDC-4C65-8954-58F5F293FAFD
PageTitle: TypeScript Programming with Visual Studio Code
DateApproved: 4/14/2016
MetaDescription: Get the best out editing TypeScript with Visual Studio Code.
---

# Editing TypeScript

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.
It offers classes, modules, and interfaces to help you build robust components. A language specification can be found [here](https://github.com/Microsoft/TypeScript/tree/master/doc).

TypeScript是JavaScript的超集，它编译出的文件也是JavaScript。
它支持类，模块，接口，更易于构建组件。说明文档地址：[Github](https://github.com/Microsoft/TypeScript/tree/master/doc).

VS Code's TypeScript support can operate in two different modes:

VS Code's TypeScript 支持2种操作模式

* **File Scope**: in this mode TypeScript files opened in Visual Studio Code are treated as independent units. As long as a file `a.ts` doesn't reference a file `b.ts` explicitly (either using [/// reference directives](http://www.typescriptlang.org/docs/handbook/triple-slash-directives.html) or external modules) there is no common project context between the two files.
* **文件域**：在VSCode中，文件浏览模式的TypeScript文件是以单个文件的形式存在的，所以不会存在`a.ts`引用`b.ts`的情况。

* **Explicit Project**: a TypeScript project is defined via a `tsconfig.json` file. The presence of such a file in a directory indicates that the directory is the root of a TypeScript project. The file itself lists the files belonging to the project as well as compiler options. Details about the `tsconfig.json` file can be found [here](https://github.com/Microsoft/TypeScript/wiki/tsconfig.json).
* **明确项目**：通过一个`tsconfig.json`文件定义的TypeScript项目，这个文件所在的目录就是项目的根目录。这个文件列举出了项目的所有文件和编译选项。关于`tsconfig.json`的详细信息可以在[这里](https://github.com/Microsoft/TypeScript/wiki/tsconfig.json)看到。

>**Tip:** We recommend that you use explicit projects over file scope projects. Since explicit projects list the files belonging to a project language, features like `Find All References` `kb(editor.action.referenceSearch.trigger)` consider the project scope and not the file scope only.

>**提示：** 我们更推荐大家使用项目而不是文件，因为明且的项目将会地处属于这个项目的语言文件，就像 `Find All References` `kb(editor.action.referenceSearch.trigger)` 将会考虑项目的范围而不仅仅是文件范围。

## tsconfig.json

Typically the first step in any new TypeScript project is to add in a `tsconfig.json` file.  This defines the TypeScript project settings such as the compiler options and the files that should be included.  To do this, open up the folder where you want to store your source and add in a new file named `tsconfig.json`.  Once in this file IntelliSense will help you along the way.

首先我们都会为每个新的TypeScript项目添加一个`tsconfig.json`文件，它定义了项目的配置，比如编译选项和应该包含的文件，为此，打开你想储存源文件的文件夹并添加一个名为`tsconfig.json`文件。只要在这个文件智能感应将会一直帮助你。

![jsconfig.json IntelliSense](images/typescript/jsconfigintellisense.png)



A simple `tsconfig.json` looks like this for ES5, **CommonJS** [modules](http://www.commonjs.org/specs/modules/1.0) and source maps:

一个简单 ES5 `tsconfig.json` 应该像这样，包含了**CommonJS** [模块](http://www.commonjs.org/specs/modules/1.0) 和 source maps：

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true
    }
}
```

Now when you create a `.ts` file as part of the project we will offer up rich editing experiences and syntax validation.

当你创建项目的一个`.ts`文件，我们将会提供给你丰富的编辑体验和语法检查。


## Transpiling TypeScript into JavaScript

将TypeScript转化为JavaScript

VS Code integrates with `tsc` through our integrated [task runner](/docs/editor/tasks.md).  We can use this to transpile `.ts` files into `.js` files.  Let's walk through transpiling a simple TypeScript Hello World program.

通过我们集成的[task runner](/docs/editor/tasks.md)来集成VSCode和`tsc`。让我们通过Hello World程序来了解下转化过程。

### Step 1: Create a simple TS file

### 第一步：创建一个TS文件

Open VS Code on an empty folder and create a `HelloWorld.ts` file, place the following code in that file...

打开VSCode，在一个空目录下创建一个`HelloWorld.ts`文件，在文件内加入以下代码...

``` typescript
class Startup {
    public static main(): number {
        console.log('Hello World');
        return 0;
    }
}

Startup.main();
```

### Step 2: Create tasks.json
### 第二步：创建task.json文件

The next step is to set up the task configuration.  To do this open the **Command Palette** with `kb(workbench.action.showCommands)` and type in **Configure Task Runner**, press `kbstyle(Enter)` to select it. This shows a selection box with templates you can choose from:

下一步就是创建任务配置。首先要用`kb(workbench.action.showCommands)`打开**Command Palette**写入**Configure Task Runner**，按下`kbstyle(Enter)`选择。这里显示了你可以选择的模版复选框。



![Task Runner Selection](images/typescript/taskSelection.png)

Select TypeScript - tsconfig.json. This will create a `tasks.json` file in the workspace `.vscode` folder.

选择 TypeScript - tsconfig.json。这将会在工作空间的.vscode目录下创建一个task.json文件。

The content of the tasks.json file looks like this:

task.json文件的内容像这样：

```json
{
	// See http://go.microsoft.com/fwlink/?LinkId=733558
	// for the documentation about the tasks.json format
	"version": "0.1.0",
	"command": "tsc",
	"isShellCommand": true,
	"args": ["-p", "."],
	"showOutput": "silent",
	"problemMatcher": "$tsc"
}
```

> **Tip:** While the template is there to help with common configuration settings, IntelliSense is available for the `tasks.json` file as well to help you along.  Use `kb(editor.action.triggerSuggest)` to see the available settings.

> **提示：**这个模版有助于常用配置的设置，task.json的智能感应可以很好的帮到你，使用`kb(editor.action.triggerSuggest)`去查看可用配置。


Under the covers we interpret `tsc` as an external task runner exposing exactly one task: the compiling of TypeScript files into JavaScript files. The command we run is: `tsc -p .`

在这里，我们的解读`tsc`是一个外部的task runner执行了这样的任务：将TypeScript文件编译为JavaScript文件。执行的命令为：`tsc -p .`


>**Tip:** If you don't have the TypeScript compiler installed, you can [get it here](http://www.typescriptlang.org/).

>**提示:** 如果你没有安装TypeScript编译器，你可以点击[这里](http://www.typescriptlang.org/)。

### Step 3: Run the Build Task
###第三步：执行构建任务

As this is the only task in the file, you can execute it by simply pressing `kb(workbench.action.tasks.build)` (**Run Build Task**).  At this point you will see an additional file show up in the file list `HelloWorld.js`.

因为这是在文件的唯一任务，你可以直接按下`kb(workbench.action.tasks.build)` (**Run Build Task**)执行。这时候你将会看到文件列表额外多了一个`HelloWorld.js`文件。

The example TypeScript file did not have any compile problems, so by running the task all that happened was a corresponding `HelloWorld.js` and `HelloWorld.js.map` file was created.

TypeScript的示例文件不会有任何的编译问题，所以运行该任务将会生成一个相应的 `HelloWorld.js` 并创建一个 `HelloWorld.js.map` 文件。

If you have [Node.js](https://nodejs.org) installed, you can run your simple Hello World example by opening up a terminal and running:

如果你安装了 [Node.js](https://nodejs.org)，你可以打开一个的终端并执行如下命令来运行你的Hello World示例：

```
node HelloWorld.js
```

> **Tips** You can also run the program using VS Code's Run/Debug feature. Details about running and debugging node apps in VS Code can be found [here](/docs/runtimes/nodejs#_debugging-your-node-application)

> **提示:** 你也可以使用VS Code's的执行/调试功能运行代码。[这里](/docs/runtimes/nodejs#_debugging-your-node-application)可以看到在VS Code执行和调试node应用的细节。


### Step 4: Reviewing Build Issues
###第四步：检查构建问题

Unfortunately, most builds don't go that smoothly and the result is often some additional information.  For instance, if there was a simple error in our TypeScript file, we may get the following output from `tsc`:

不幸的是，大多情况下构建都不会太顺利并且结果将会返回额外的信息。比如，如果一个简单的错误在我们的TypeScript文件里面， `tsc` 可能会使我们得到下面的输出：

    HelloWorld.ts(3,17): error TS2339: Property 'logg' does not exist on type 'Console'.

This would show up in the output window (which can be opened using `kb(workbench.action.output.toggleOutput)`) and selecting Tasks in the output view dropdown.  We parse this output for you and highlight detected problems in the Status Bar.

信息将会在输出窗口显示出来(它可以用`kb(workbench.action.output.toggleOutput)`打开)还可以在输出视口的下拉列表内选择任务，我们会将输出解析并在状态栏内高亮检测出的问题。

![Problems in Status Bar](images/typescript/problemstatusbar.png)

You can click on that icon to get a list of the problems and navigate to them.

你可以通过点击图标得到问题列表并导航到他们。

![Compile Problems](images/typescript/compileerror.png)

You can also use the keyboard to open the list `kb(workbench.action.showErrorsWarnings)`.

你也可以使用键盘打开问题列表`kb(workbench.action.showErrorsWarnings)`

>**Tip:** Tasks offer rich support for many actions. Check the [Tasks](/docs/editor/tasks.md) topic for more information on how to configure them.

>**提示:** Tasks提供了很多动作的支持，[Tasks](/docs/editor/tasks.md) 将得到很多配置他们的信息.

## Goto Symbol & Show All Symbols
## 跳转到符号 & 显示所有符号

`kb(workbench.action.gotoSymbol)`: lists all defined symbols of the current open TypeScript and lets you navigate in it.

`kb(workbench.action.gotoSymbol)`:列出了当前打开TypeScript的所有定义的符号并让能自动导航到那里。

`kb(workbench.action.showAllSymbols)`: lets you search all symbols defined in the current project or file scope. You need to have a TypeScript file open in the active editor.

`kb(workbench.action.showAllSymbols)`:让您可以搜索在当前项目或文件的范围内定义的所有符号。在活动的编辑区你需要有一个打开的TypeScript文件。

## Format Code

## 格式代码

`kb(editor.action.format)`: formats the currently selected code, or the whole document if no code is selected.

`kb(editor.action.format)`: 格式当前选中的代码，如果没有代码选中将会格式化整个文档。

## JSDoc Support

### JSDoc 支持

VS Code offers **JSDoc** support for TypeScript. Besides syntax coloring, we help you enter **JSDoc** comments. Simply type `/**` and it will auto insert the closing `*/`. Pressing `kbstyle(Enter)` inside a **JSDoc** block will indent the next line and auto insert a `*`.

VS Code为TypeScript提供 **JSDoc** 支持。除了语法着色，还加入了 **JSDoc** 注释。只需要输入 `/**` 将会自动添加 `*/` 。在 **JSDoc** 块内按下 `kbstyle(Enter)` 将会在下一行缩进并且自动添加 `*`。

## JavaScript Source Map Support

## JavaScript Source Map 支持

TypeScript debugging supports JavaScript source maps. Enable this by setting the `sourceMaps` attribute to `true` in the project's launch configuration file `launch.json`. In addition, you can specify a TypeScript file with the `program` attribute.

TypeScript 调试支持JavaScript source maps。开启方式是将配置文件 `launch.json` 的 `sourceMaps` 属性设置为 `true` 。另外，你也可以指定TypeScript文件的 `program` 变量。

To generate source maps for your TypeScript files, compile with the `--sourcemap` option or set the `sourceMap` property in the `tsconfig.json` file to `true`.

要生成TypeScript文件的source maps，需要使用 `--sourcemap` 选项编译或者设置 `tsconfig.json` 文件的 `sourceMap` 属性为 `true` 。

In-lined source maps (a source map where the content is stored as a data URL instead of a separate file) are also supported, although in-lined source is not yet supported.

In-lined source maps (一个内容存储在URL而不是以单独文件存储的source map)也被支持，虽然in-lined source还未被支持。


## Setting a different outDir for generated files

##设置为生成的文件设置不同的输出目录

If generated (transpiled) JavaScript files do not live next to their source, you can help the VS Code debugger locate them by specifying the outDir directory in the launch configuration. Whenever you set a breakpoint in the original source, VS Code tries to find the generated source, and the associated source map, in the outDir directory.

如果生成的JavaScript文件没有出现在源代码旁边，你可以通过VS Code调试器的launch配置中输出目录。无论什么时候你都可以在输出目录中生成的源代码或者关联的source map中打断点。

## Hiding Derived JavaScript Files

## 隐藏派生的JavaScript Files

When you are working with TypeScript, you often don’t want to see generated JavaScript files in the explorer or in search results. VS Code offers filtering capabilities with a `files.exclude` [setting](/docs/customization/userandworkspace.md) (**File** > **Preferences** > **Workspace Settings**) and you can easily create an expression to hide those derived files:

当你使用TypeScript工作的时候，尝尝不希望在资源管理器或者搜索结果中看到生成的JavaScript文件。VS Code通过`files.exclude` [setting](/docs/customization/userandworkspace.md) (**File** > **Preferences** > **Workspace Settings**) 提供了文件过滤功能，你可以轻松创建隐藏这些导出的文件的表达式。

`"**/*.js": { "when": "$(basename).ts"}`

This pattern will match on any JavaScript file (`**/*.js`) but only if a sibling TypeScript file with the same name is present. The file explorer will no longer show derived resources for JavaScript if they are compiled to the same location.

这个模式将会匹配所有的JavaScript文件(`**/*.js`)但是只显示相同名字的兄弟TypeScript文件，如果他们被编译到一起文件资源管理器不会显示派生的JavaScript资源。

![Hiding derived resources](images/typescript/hidingDerivedBefore.png) ![Hiding derived resources](images/typescript/hidingDerivedAfter.png)

## Mixed TypeScript and JavaScript projects

## TypeScript和JavaScript混合项目

It is now possible to have mixed TypeScript and JavaScript projects. To enable JavaScript inside a TypeScript project, you can set the `allowJs` property to `true` in the `tsconfig.json`.

现在已经可能存在TypeScript和JavaScript混合的项目。要开启JavaScript在TypeScript项目，你可以在 `tsconfig.json` 中设置 `allowJs` 属性为 `true` 

>**Tip:** The `tsc` compiler does not detect the presence of a `jsconfig.json` file automatically. Use the `–p` argument to make `tsc` use your `jsconfig.json` file, e.g. `tsc -p jsconfig.json`.

>**提示：**  `tsc` 不会自动检测 `jsconfig.json` 文件是否存在，使用 `tsc` 的 `–p` 参数去生成自己的 `jsconfig.json` 文件，如 `tsc -p jsconfig.json`。

## Using Newer TypeScript Versions

## 使用新版本的TypeScript

VS Code ships with a recent stable version of TypeScript in the box.  If you want to use a newer version of TypeScript, you can define the `typescript.tsdk` setting (**File** > **Preferences** > **User/Workspace Settings**) pointing to a directory containing the TypeScript `tsserver.js` and the corresponding `lib.*.d.ts` files. The directory path can be absolute or relative to the workspace directory. By using a relative path, you can easily share this workspace setting with your team and use the latest TypeScript version (`npm install typescript@next`). Refer to this [blog post](https://blogs.msdn.com/b/typescript/archive/2015/07/27/introducing-typescript-nightlies.aspx) for more details on how to install the nightly builds of TypeScript.

VS Code 附带了最近稳定版本的TypeScript。如果你想要使用最近版本的TypeScript，你可以定义一个 `typescript.tsdk` 环境 (**File** > **Preferences** > **User/Workspace Settings**) 指定一个包涵TypeScript `tsserver.js` 和 对应的 `lib.*.d.ts` 文件的目录。

## Next Steps

## 下一步

OK, read on to find out about:

好，继续阅读深入了解：

* [JavaScript](/docs/languages/javascript.md) - we have several JavaScript specific features in VS Code
* [Tasks](/docs/editor/tasks.md) - we used tasks to transpile your TS file. Read more to find out what else tasks can do
* [Editing Evolved](/docs/editor/editingevolved.md) - dig into multi-cursor, snippets and more
* [Debugging](/docs/editor/debugging.md) - we support debugging TypeScript Node.js apps

## Common Questions

## 通常都会遇到的问题

**Q: How do I resolve a TypeScript "Cannot compile external module" error?**

## 问题：我怎么解决TypeScript "Cannot compile external module"的错误？

**A**: If you get that error, resolve it by creating a `tsconfig.json` file in the root folder of your project. The tsconfig.json file lets you control how Visual Studio Code compiles your TypeScript code. For more information, see the [typescript.json overview](https://github.com/Microsoft/TypeScript/wiki/tsconfig.json).

**回答** 如果你遇到这个错误，可以通过在项目的根目录下创建一个 `tsconfig.json` 文件的方式解决。 你可以用过 `tsconfig.json` 文件控制VS Code怎样编译你的TypeScript代码。获取更多信息，请参阅[typescript.json overview](https://github.com/Microsoft/TypeScript/wiki/tsconfig.json)。

Due to a current limitation, you must restart VS Code after adding the `tsconfig.json` file.

由于当前有局限性，在添加 `tsconfig.json` 后你必需重启VS Code。