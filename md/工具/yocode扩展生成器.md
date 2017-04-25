---
Order: 2
Area: tools
TOCTitle: Extension Generator
ContentId: C733425A-3F06-4DB9-90A0-472EF1DB58D3
PageTitle: The Yo Code Visual Studio Code Extension Generator
DateApproved: 4/14/2016
MetaDescription: Easily create VS Code extensions and customizations with the Yo Code generator.
---
# Yo Code - Extension Generator    
# Yo Code - 扩展生成器

We have written a Yeoman generator to help get you started.    
我们写一个Yeoman生成器来作为开始。

## Install the Generator   
## 安装生成器   

Install Yeoman and the VS Code Extension generator from the command prompt:   
从命令行安装Yeoman和VSCode扩展生成器：

```bash
npm install -g yo generator-code
```

## Run Yo Code   
## 运行Yo Code

The Yeoman generator will walk you through the steps required to create your customization or extension prompting for the required information.    
Yeoman生成器会要求你一步步的填写相应信息来创建自定义或扩展的提示。

To launch the generator simply type the following in a command prompt:   
在命令行中输入如下命令来启动生成器：

```bash
yo code
```

![yo code output](images/yocode/yocode.png)

## Generator Options   
## 生成器选项

The generator can either create an extension skeleton for a new extension or create a ready-to-use extension for languages, themes or snippets based on existing TextMate definition files.    
生成器可以为新的扩展创建一个扩展框架或者基于已经存在的TextMate定义文件为语言、主题和片段创建一个准备使用的扩展，

### New Extension in TypeScript   
### 使用TypeScript写新扩展

Creates an extension skeleton implementing a 'hello world' command. Use this as a starting point for your own extension.   
创建一个扩展框架实现'hello world'命令。用这个作为开发你自己的扩展的起点。

* Prompts for the extension identifier and will create a folder of that name in the current directory    
* 提示在当前目录下创建一个以扩展标识为名称的文件夹
* Creates a base folder structure with a source, test and output folder   
* 创建包含source、test和output文件夹的基础文件夹结构
* Templates out a `package.json` file and an extension main file    
* 生成一份`package.json`模板和扩展主文件
* Sets-up `launch.json` and `tasks.json` so that F5 will compile and run your extension and attach the debugger    
* 配置`launch.json`和`tasks.json`使得按F5就能编译和运行你的扩展，以及挂载调试器
* Optionally sets up a Git repository   
* 可以选择配置一个Git仓库

Once created, open VS Code on the created folder. The folder contains a file `vsc-extension-quickstart.md` as a quick guide with the next steps. The extension is setup so that you get IntelliSense for the extension API.    
创建成功后，打开这个被创建的文件夹。文件夹包含一个`vsc-extension-quickstart.md`文件作为后续步骤的快速指南。扩展会为你配置扩展API的智能提示。

### New Extension in JavaScript   
### 使用JavaScript写新扩展

Does the same as `New Extension (TypeScript)`, but for JavaScript. The extension is setup so that you get IntelliSense for the extension API.    
和`New Extension (TypeScript)`一样，但是是为JavaScript写的。扩展会为你配置扩展API的智能提示。

### New Color Theme   
### 新的颜色主题

Creates an extension that contributes a new color theme based on an existing TextMate color theme.    
基于已存在的TextMate颜色主题为扩展贡献一个新的颜色主题。

* Prompts for the location (URL or file path) of the existing TextMate color theme (.tmTheme). This file will be imported into the new extension.    
* 提示输入现有的TextMate颜色主题(.tmTheme)的位置（URL或者文件路径)。
* Prompts for the color theme name as well as the color base theme (light or dark)   
* 提示为这个基本的颜色主题(light or dark)输入名称。
* Prompts for the extension identifier and will create a folder of that name in the current directory    
* 提示在当前目录下创建一个以扩展标识为名称的文件夹

Once created, open VS Code on the created folder and run the extension to test the new theme.    
创建成功后，用VSCode打开这个文件夹并运行扩展来测试这个新主题。
Check out `vsc-extension-quickstart.md`. It's a quick guide with the next steps.    
查看`vsc-extension-quickstart.md`。它是后续步骤的快速指南。

### New Language Support    
### 新语言支持

Creates an extension that contributes a language with colorizer.    
为带着色器的语言创建一个扩展。

* Prompts for the location (URL or file path) of an existing TextMate language file (.tmLanguage, .plist or .json). This file will be imported to the new extension    
* 提示输入现有的TextMate语言文件(.tmLanguage, .plist or .json)的位置（URL或者文件路径）。这个文件将被导入到新的扩展
* Prompts for the extension identifier and will create a folder of that name in the current directory    
* 提示在当前目录下创建一个以扩展标识为名称的文件夹

Once created, open VS Code on the created folder and run the extension to test the colorization. Check out `vsc-extension-quickstart.md` for the next steps. Have a look at the language configuration file that has been created and defines configuration options such what style of comments and brackets the language uses.     
创建成功后，用VSCode打开这个文件夹并运行扩展来测试着色。查看`vsc-extension-quickstart.md`文件了解后续步骤。看看已经创建的语言配置文件，并定义语言使用什么样的注释和括号。

### New Code Snippets   
### 新代码段

Creates an extension that contributes new code snippets.    
为新代码段创建一个扩展。

* Prompts for the folder location that contains TextMate snippets (.tmSnippet) or Sublime snippets (.sublime-snippet). These file are converted to a VS Code snippet file.    
* 提示输入已有的TextMate片段(.tmSnippet)或者Sublime片段(.sublime-snippet)的位置。这些文件会被转换成VSCode代码段文件。
* Prompts for the language for which these snippets will be active    
* 提示输入被激活的代码段的语言
* Prompts for the extension identifier and will create a folder of that name in the current directory   
* 提示在当前目录下创建一个以扩展标识为名称的文件夹

Once created, open VS Code on the created folder and run the extension to test the snippets. Check out `vsc-extension-quickstart.md` for the next steps.    
创建成功后，用VSCode打开这个文件夹并运行扩展来测试这个片段。查看`vsc-extension-quickstart.md`文件了解后续步骤

## Loading an Extension   
## 加载扩展

To load an extension, you need to copy the files to your VS Code extensions folder. We cover this in detail here: [Installing Extensions](/docs/extensions/install-extension.md#your-extensions-folder).    
要加载扩展，你需要复制一些文件到你的VSCode扩展文件夹。 我们在这里进行详细介绍: [安装扩展](/docs/extensions/install-extension.md#your-extensions-folder)。

## Next Steps   
## 后续步骤

* [Publishing Tool](/docs/tools/vscecli.md) - Learn how to publish your extensions to the VS Code Marketplace   
* [发布工具](/docs/tools/vscecli.md) - 学习如何将你的扩展发布到商店中
* [Hello World](/docs/extensions/example-hello-world.md) - Try the 'Hello World' walkthrough to build your first extension   * [Hello World](/docs/extensions/example-hello-world.md) - 尝试'Hello World'演练作为你的第一个扩展

## Common Questions  
## 常见问题

**Q: The `yo code` generator doesn't respond to arrow keys on Windows 10.**    
**问题: `yo code`在Win10中不返回许可Keys。**

**A:** Try starting the Yeoman generator with just `yo` and then select the `Code` generator.    
**回答:** 尝试仅适用`yo`启动Yeoman生成器然后再选择`Code`生成器。

![yo workaround](images/yocode/yo-workaround.png)
