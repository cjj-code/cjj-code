---
title: python处理excel文件
date: 2022-09-12 20:21:20
cover: /images/posts/python处理excel文件/2022-09-12-20-31-33.png
tags:
    - python
    - excel
categories:
    - python/进阶
---
## 常用库

- openpyxl：目前最常用excel处理第三方库
- xlrd：读取excel的库，只有1.2.0之前的版本支持xlsx格式
- pandas：数据分析专用，可以处理Excel文件

## 概述

### 介绍

openpyxl 是一个 Python 库，用于读取/写入 Excel 2010 xlsx/xlsm/xltx/xltm 文件。

**三个概念**：`Workbook`,`Sheet`,`Cell`

- Workbook就是一个excel工作表
- Sheet是工作表中的一张表
- Cell就是一个单元格

**官方文档：**https://openpyxl.readthedocs.io/en/stable/tutorial.html

### 安装

```bash
$ pip install openpyxl
```

优质博客教程：https://blog.csdn.net/m0_47170642/article/details/119137885



## 常用属性和方法

1. workbook对象 - 工作簿

    声明`wb = openpyxl.Workbook()`

    - `wb.active`：创建工作表时会默认创建一个表格，使用active属性获取
    - `wb.create_sheet`：额外创建一个表格
    - `wb.sheetnames`：获取所有的表格名
    - `wb.copy_worksheet()`：创建一个工作表副本

2. sheet对象 - 工作表

    声明`ws = wb.active`或`ws = wb['表格名称']`

    - `ws.title`：表格的标题，默认是Sheet、Sheet1、Sheet2、...

    - `ws.rows：`按行获取单元格，返回的是cell对象组成的元祖，cols属性同理
    - `ws.columns`：按列获取单元格
    - `ws.values`：按行获取表格内的数据，返回的是元祖
    - `ws.iter_rows()`：按行获取所有的单元格
    - `ws.iter_cols()`：按列获取所有的单元格
    - `ws.cell()`：设置单元格的值
    - `ws.append()`：向表格中写入一行数据（传入列表）

3. cell对象 - 单元格

    - `cell.row`：获取单元格所在的行
    - `cell.column`：获取单元格所在的列
    - `cell.value`：获取单元格里的值



## 基本操作

### 常见流程

创建一个Excel文件

```python
from openpuxl import Workbook
book = Wrokbook()
sheet = book.active  #或者使用book.create_sheet('名称', 0)指定表单名称和位置
...
book.save("*.xlsx")
```

读取一个Excel文件

```python
from openpyxl import load_workbook
book = load_workbook('*.xlsx')
sheet = book['Sheet1']
...
```

### sheet表单操作

遍历行

```python
import openpyxl
book = openpyxl.load_workbook('*.xlsx')
sheet = book['表单名']           # book.get_sheet_by_name方式已被弃用
for line in sheet.rows:
    item_data = [i.value for i in line]
    print(item_data)
```

### 单元格操作

#### 通过下标

- 一个单元格：`ws['A4']`
- 多个单元格
    - 切片获取单元格范围：`ws['A1':'C2']`
    - 一列：`ws['B']`
    - 一行：`ws[10]`

#### `Worksheet.iter_rows()`方法

#### `Worksheet.cell()`方法



## 常见业务场景

### 场景一：将数据以excel表格形式输出

```python
from openpuxl import Workbook
wb = Wrokbook()
ws = wb.active  # 或者使用book.create_sheet('名称', 0)指定表单名称和位置

for item_data in data:  # data为数据来源，必须是可迭代对象
    ws.append(item_data)

wb.save("*.xlsx")
```

### 场景二：读写较大的Excel文件

当excel文件过大时，常规处理方式openpyxl可能无法处理，需要使用`只读`/`只写`来延迟加载，但处理完成后需要使用`wb.close()`来手动关闭工作簿

1. 只读模式

    ```python
    from openpyxl import load_workbook
    wb = load_workbook(filename='large_file.xlsx', read_only=True) # 设置打开方式为只读
    ws = wb['big_data']
    
    for row in ws.rows:
        for cell in row:
            print(cell.value)
    
    wb.close()
    ```

2. 只写模式

    ```python
    from openpyxl import Workbook
    wb = Workbook(write_only=True) # 设置打开方式为只写
    ws = wb.create_sheet()
    
    for irow in range(100):
    	ws.append(['%d' % i for i in range(200)])
    
    wb.save('new_big_file.xlsx')
    ```

    > - 与普通工作簿不同，新创建的只写工作簿不包含任何工作表；必须使用该`create_sheet()`方法专门创建工作表。
    > - 在只写工作簿中，行只能使用 `append()`. 使用 或 无法在任意位置写入（或读取）单元`cell()`格`iter_rows()`。
    > - 它能够导出无限量的数据（甚至超过 Excel 实际可以处理的数据），同时将内存使用量保持在 10Mb 以下。
    > - 只写工作簿只能保存一次。之后，每次将工作簿或 append() 保存到现有工作表的尝试都会引发[`openpyxl.utils.exceptions.WorkbookAlreadySaved`](https://openpyxl.readthedocs.io/en/stable/api/openpyxl.utils.exceptions.html#openpyxl.utils.exceptions.WorkbookAlreadySaved) 异常。
    > - 在实际单元格数据之前出现在文件中的所有内容都必须在添加单元格之前创建，因为它必须在此之前写入文件。例如，应该在添加单元格之前设置freeze_panes 。

### 场景三：在表格后追加一列数据

### 场景四：合并两个表格
参考文章：https://zhuanlan.zhihu.com/p/259583430