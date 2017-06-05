---
Order: 11
Area: languages
TOCTitle: Dockerfile
ContentId: 42F8B9F8-BD03-4159-9479-17C5BDE30531
PageTitle: Working with Dockerfiles in Visual Studio Code
DateApproved: 4/14/2016
MetaDescription: Find out how to get the best out of Visual Studio Code and Docker.
---

# 使用Docker工作

[Docker](http://www.docker.com) 是现今十分热门的容器引擎，可以让你轻松地打包、部署和使用应用程序以及服务。无论你是一个经验丰富的Docker开发者还是刚刚开始学习它，Visual Studio Code都可以让你轻松地创造`Dockerfile`和`docker-compose.yml`两个文件到你的开发目录中。

## 安装Docker扩展插件

VS Code通过插件的方式支持Docker的使用。安装这一扩展插件，只需要按下`kb(workbench.action.showCommands)`，然后输入"ext install"并且运行**Extensions: Install Extension**命令来获得目前支持的插件列表。现在输入docker搜索所需插件然后选择[Dockerfile and Docker Compose File (yml) Support](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker)插件。

![Select Docker extension](images/docker/installdockerextension.png)

## Dockerfiles

通过Docker，你可以指定一系列的命令，通过它们在`Dockerfile`中建立镜像。一个Dockerfile是包含着一系列安装指令的文本脚本。

VS Code 很清楚Dockerfiles的结构以及可以使用的指令集，这意味着当你使用VS Code编辑这些文件时它可以给予你很多的经验指导。

1. 在你的工作目录中创建一个新的文件命名为`Dockerfile`
2. 按下`kb(editor.action.triggerSuggest)`来获得`Dockerfile`中命令的补全

 ![Dockerfile snippets](images/docker/dockerfileintellisense.png)

3. 按下`kbstyle(Tab)`在段落中不同的区域移动。比如说，在`COPY`部分你可以输入`source`，接着按下`kbstyle(Tab)`移动到`dest`部分。

 ![Dockerfile snippet navigation](images/docker/dockerfiletemplate.png)

除了编辑`Dockerfile`时的各种功能，当你防止鼠标在一个Docker命令上的时候，Visual Studio Code将会提供关于这个命令的描述。比如说，当你的鼠标放到`WORKDIR`上面的时候你将可以看到以下描述。

![Dockerfile hover tooltip](images/docker/dockerfiletooltip.png)

想要获取更多关于Dockerfiles的信息，可以进入在[docker.com](http://docker.com)上面的[Dockerfile best practices](
https://docs.docker.com/articles/dockerfile_best-practices/)

## Docker compose

[Docker Compose](https://docs.docker.com/compose/)让你可以通过Docker定义以及运行多容器应用。你可以通过一个叫做`docker-compose.yml`的文件来定义容器的外形。

对于`docker-compose.yml`的经验，Visual Studio Code的功能同样也是十分丰富的。它可以为合法的Docker compose指令提供IntelliSense和在帮助你查询Docker Hub找到适合的镜像。

1. 在你的工作目录中创建一个名为`docker-compose.yml`的新文件
2. 定义一个新的服务成为`web:`
3. 在第二行，通过`kb(editor.action.triggerSuggest)`引入IntelliSense来查看所有合法的指令列表

 ![Docker Compose IntelliSense](images/docker/dockercomposeintellisense.png)


4. 对于`image`指令，你可以再次输入`kb(editor.action.triggerSuggest)`来完成，而且VS Code会帮你在Docker Hub上查询公开的镜像。

 ![Docker Compose image suggestions](images/docker/dockercomposeimageintellisense.png)

VS Code 第一次使用会根据一些元数据比如说star的数量和描述去为你显示一系列热门的镜像。如果你继续输入，VS code会查询Docker Hub的索引去找到更加符合的镜像，包括搜索公开的profiles。比如说，搜索`Microsoft`会显示所有微软的镜像。

 ![Docker Compose Microsoft image suggestions](images/docker/dockercomposesearch.png)
