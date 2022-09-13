---
title: vscode图片插件paste-image
date: 2022-09-04 20:57:34
cover: images/posts/vscode图片插件paste-image/2022-09-11-14-15-34.png
tags: 
    - vscode
    - markdown
categories:
    - 环境
---

# 说明

Markdown神器typora现在已经开始收费，而且最后一个免费版本也无法正常使用，眼下最好的替代品就是vscode了，typora最大的优点之一在于对图片的处理，可以将粘贴板中的图片直接保存到设置的目录下面。
其实vscode也能实现类似的功能，但需要安装插件，以下便介绍该插件的用法。

# 插件

在vscode插件商店搜索`Paste Image`

![](/images/posts/vscode图片插件paste-image/2022-09-11-14-23-29.png)

或者从官网下载导入vscode

官网地址：https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image

粘贴图片时，windows使用快捷键`Ctrl+Alt+V`， mac使用快捷键`Cmd+Alt+V`

# 配置

## 配置方法

进入vscode插件板块，找到已安装的插件，右击选择拓展设置

![](/images/posts/vscode图片插件paste-image/2022-09-13-22-50-28.png)

进入插件设置后如下

![](/images/posts/vscode图片插件paste-image/2022-09-13-22-51-24.png)

注意：

- `用户`选项卡设置的是全局配置
- `工作区`选项卡内的设置只对当前工作目录有效，并且更改默认设置后，会在当前工作目录下创建`.vscode/settings.json`文件


## 常用配置选项

大部分摘自[官网](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image)

### pasteImage.defaultName

默认图像文件名。

此配置的值将传递给 moment 库（一个 js 时间操作库）的 'format' 函数，您可以阅读文档https://momentjs.com/docs/#/displaying/format/以了解高级用法。

你可以使用变量：

- `${currentFileName}`: 当前文件名带后缀
- `${currentFileNameWithoutExt}`: 当前文件名，不带后缀
默认值为Y-MM-DD-HH-mm-ss。

### pasteImage.path

图像保存的位置

可使用变量：
- `${currentFileDir}`: 包含当前编辑文件的目录路径
- `${projectRoot}`：在vscode中打开的项目的路径
- `${currentFileName}`: 当前文件名带后缀
- `${currentFileNameWithoutExt}`: 当前文件名，不带后缀

### pasteImage.basePath

图片url的基本路径
若图片url采用相对路径，这个属性设置的就是相对路径对应的根目录

可使用变量：
- `${currentFileDir}`: 包含当前编辑文件的目录路径
- `${projectRoot}`：在vscode中打开的项目的路径
- `${currentFileName}`: 当前文件名带后缀
- `${currentFileNameWithoutExt}`: 当前文件名，不带后缀

### pasteImage.prefix

在粘贴之前将字符串添加到解析的图像路径

默认为""


# 常用配置记录

## 日常文档书写

**预期效果**：

在当前编辑的Markdown文件目录下的`image`文件夹内存放图片。

```shell
$ tree . -a
.
├── .vscode
│   └── settings.json
├── image
│   ├── 2022-09-13-23-07-49.png
│   └── ...
└── 如何娶到富婆.md
```

**配置**：

`.vscode/settings.json`文件配置如下

```json
{
    "pasteImage.path": "${currentFileDir}/image",
    "pasteImage.prefix": "./"
}
```

## 个人笔记

**预期效果**:

当前工作目录下有多个Markdown笔记，每篇文章的图片放在image/文件名/文件夹下，

```shell
$ tree . -a
.
├── .vscode
│   └── settings.json
├── image
│   ├── 如何打倒ws
│   │   └── 2022-09-13-23-24-59.png
│   ├── 如何一夜暴富
│   │   └── 2022-09-13-23-25-43.png
│   └── 如何娶到富婆
│       └── 2022-09-13-23-25-17.png
├── 如何打倒ws.md
├── 如何一夜暴富.md
└── 如何娶到富婆.md
```

**配置**

`.vscode/settings.json`文件配置如下

```json
{
    "pasteImage.path": "${currentFileDir}/image/${currentFileNameWithoutExt}",
    "pasteImage.prefix": "./"
}
```



## Hexo博客

**预期效果**：

官网的要求

![](/images/posts/vscode图片插件paste-image/2022-09-13-21-16-36.png)

**配置**：

在Hexo博客项目根目录下，`.vscode/settings.json`文件配置如下

```json
{
    "pasteImage.path": "${projectRoot}/source/img",
    "pasteImage.basePath": "${projectRoot}/source",
    "pasteImage.forceUnixStyleSeparator": true,
    "pasteImage.prefix": "/"
}
```

这种方式也有弊端，每篇文章的图片放到同一个文件夹下，跟图床一样不能很好地管理每篇文章的图片，于是我在搭建这个博客站的时候采取了了如下的优化方案：

## Hexo博客（优化方案）

**预期效果**：

image资源文件夹下，创建posts文件夹存放博客相关图片，每篇文章在image/posts中都有一个同名文件夹用来存放该文章的图片 
![](/images/posts/vscode图片插件paste-image/2022-09-13-21-42-07.png) 

**配置**：

实现上述效果的配置如下
```json
{
    "pasteImage.path": "${projectRoot}/source/images/posts/${currentFileNameWithoutExt}",
    "pasteImage.basePath": "${projectRoot}/source",
    "pasteImage.prefix": "/"
}
```