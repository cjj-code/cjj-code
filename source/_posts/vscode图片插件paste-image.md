---
title: vscode图片插件paste-image
date: 2022-09-04 20:57:34
cover: 
tags: 
    - vscode
---

# 说明

Markdown神器typora现在已经开始收费，而且最后一个免费版本也无法正常使用，最好的替代品就是vscode了，typora最大的优点之一在于对图片的处理，可以将粘贴板中的图片直接保存到设置的目录下面。
其实vscode也能实现类似的功能，但需要安装插件，以下便介绍该插件的用法。

# 常用配置

### pasteImage.path

图像保存的位置

可使用变量：
- ${currentFileDir}: 包含当前编辑文件的目录路径
- ${projectRoot}：在vscode中打开的项目的路径
- ${currentFileName}: 当前文件名带后缀
- ${currentFileNameWithoutExt}: 当前文件名，不带后缀

### pasteImage.basePath

图片url的基本路径
若图片url采用相对路径，这个属性设置的就是相对路径对应的根目录

可使用变量：
- ${currentFileDir}: 包含当前编辑文件的目录路径
- ${projectRoot}：在vscode中打开的项目的路径
- ${currentFileName}: 当前文件名带后缀
- ${currentFileNameWithoutExt}: 当前文件名，不带后缀

### pasteImage.prefix

在粘贴之前将字符串添加到解析的图像路径

默认为""
