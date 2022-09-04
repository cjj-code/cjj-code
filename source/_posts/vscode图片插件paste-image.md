---
title: vscode图片插件paste-image
date: 2022-09-04 20:57:34
tags: 
    - vscode
---

# 配置

### pasteImage.path

图像保存的位置

可使用变量：
- ${currentFileDir}: 包含当前编辑文件的目录路径
- ${projectRoot}：在vscode中打开的项目的路径
- ${currentFileName}: 当前文件名带后缀
- ${currentFileNameWithoutExt}: 当前文件名，不带后缀

### pasteImage.basePath

图片url的基本路径

可使用变量：
- ${currentFileDir}: 包含当前编辑文件的目录路径
- ${projectRoot}：在vscode中打开的项目的路径
- ${currentFileName}: 当前文件名带后缀
- ${currentFileNameWithoutExt}: 当前文件名，不带后缀