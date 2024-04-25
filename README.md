

# CATAlias.ini 配置方法

CATAlias.ini 是用于配置自定义用户别名和热键的配置文件。通过掌握该配置文件的用法，用户可以自定义更适合自己需求的快捷键方案。

## 用法

1. 将提供的ini文件复制到`UCLC/user-config`目录下。
2. 打开`UCLC/config.ini`文件，将`[UserConf]`部分中的`用户别名`值更改为指定的ini文件名。
```
[UserConf]
用户别名 = CATAlias.ini  
```



## 配置文件结构

以下是用户别名配置文件的基本结构示例：

```ini
[工作台]
2001=零件设计

[通用]
M = 测量间距
A = ViewAlignment                   ; 对齐视点

[装配设计]
S = CATAifSnapHdr                   ; 捕捉

[零件设计]
S = CATMmrSketchHeaderHdr           ; 草图

[草图编辑器]
REC = CAT2DRectangleHdr             ; 矩形
CC = CAT2DCircleRadiusHdr           ; 圆

[创成式外形设计]
3C = CATFsc3DCurveHeadHdr           ; 3D 曲线

[工程制图]
CC=圆

[Generative Sheetmetal Design]
S = CATMmrSketchHeaderHdr            ; 草图

[HotKey]
; 功能键符号：
;   "^" : Ctrl
;   "+" : Shift
;   "!" : Alt
F2 = CATAfrOpenPropertyHdr              ; 属性
^+!s = CATAfrFileSaveAllAsHdr           ; 保存管理
```

**配置文件包含以下部分：**

- 工作台列表 => `[工作台]`

- 特定工作台别名  => `[装配设计]`、`[零件设计]`...

- 全局生效别名 => `[通用]`

- 组合热键 => `[HotKey]`

  

在配置文件中，`[工作台]`部分中等号右侧的值应与CATIA工作台名称一致，以准确匹配工作台并激活对应的用户别名。

`[通用]`部分中配置的用户别名在所有工作台中都可以使用。

`[HotKey]`部分配置组合快捷键的用户别名。

**Tips**

在配置文件中，同一个别名可以在多个工作台中配置，但在不同的工作台中其执行效果可能不同。例如，在零件设计工作台中，`S` 键可能是用于执行草图命令，而在装配设计工作台中，`S` 键可能被配置为执行捕捉命令。

推荐使用`command-id`来调用命令，以实现更精确的命令调用。`command-id`可以通过`工作间呈示`命令导出，[导出方法](https://zhuanlan.zhihu.com/p/367522408)可搜索相应关键字找到。



## 自定义

```
Workshop Exposition of CATAfrGeneralWks 

1- Header List 

Title= 着色 (SHD)
   Id 	= CATAfrShadingHdr
   DLL 	= CATApplicationFrame
   Cmd 	= CATFrmViewCmd
   Arg 	= <an address>   State Initial	= 1
   State Current	= 1
Title= * 仰
   Id 	= CATAfrBottomViewHdr
   DLL 	= CATApplicationFrame
   Cmd 	= CATFrmViewCmd
   Arg 	= <an address>   State Initial	= 1
   State Current	= 1
Title= 缩放
   Id 	= CATAfrZoomHdr
   DLL 	= CATApplicationFrame
   Cmd 	= CATFrmViewCmd
   Arg 	= <an address>   State Initial	= 1
   State Current	= 1
   ...
```

以上内容是通过执行`工作间呈示`命令导出的一些命令，其中的 "Id=" 字段就是我们需要的command-id

若我在配置文件的[HotKey]部分添加如下键值对：

```
^+!S = CATAfrShadingHdr
```

那么我就自定义了一个新的热键：Ctrl+Shift+Alt+S，用于执行着色（SHD）命令。