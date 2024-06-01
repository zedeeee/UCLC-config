

# 用户别名 和 快捷键 配置方法

CAT_Alias.ini 和 CAT_Hotkey.ini 是用于配置自定义用户别名和热键的配置文件。通过掌握该配置文件的用法，用户可以自定义更适合自己需求的快捷键方案。

## 用法

1. 将ini文件复制到`UCLC/user-config`目录下。
2. 打开`UCLC/config.ini`文件，将`[UserConf]`部分中的`用户别名`值更改为指定的ini文件名。
```
[UserConf]
用户别名 = CAT_Alias.ini
快捷键 = CAT_Hotkey.ini
```



## 配置文件结构

**`CAT_Alias.ini`** 用户别名配置文件的基本结构示例，只影响用户别名：

```ini
[通用]
A = ViewAlignment                   ; 对齐视点，全局生效

[零件设计]
S = CATMmrSketchHeaderHdr           ; 草图， 零件工作台生效

[草图编辑器]
CC = CAT2DCircleRadiusHdr           ; 圆，草图工作台生效
```



**`CAT_Hotkey.ini`** 快捷键配置文件的基本结构示例，只影响快捷键：

```ini
[通用]
F2 = CATAfrOpenPropertyHdr			; 属性，全局生效

[零件设计]
F7 = AsmSpaceSection                ; 切割，零件工作台生效

[草图编辑器]
!C = CATSKUSwitchEltTypeHdr         ; 构造/标准元素，草图工作台
B = command-id						; 支持定义单键热键

```

**配置文件包含以下部分：**

-  `[装配设计]`、`[零件设计]`... 只在特定工作台生效的命令


- `[通用]`配置的用户别名和快捷键在所有工作台中都可以使用。

- 可自行添加工作台，名称要与CATIA工作台按钮一致

**Tips**

在配置文件中，同一个别名/快捷键可以在多个工作台中配置，执行命令以工作台设定为准。例如，在零件设计工作台中，`S` 键可能是用于执行草图命令，而在装配设计工作台中，`S` 键可能被配置为执行捕捉命令。

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

若我在快捷键配置文件的[通用]字段添加如下键值对：

```
^+!S = CATAfrShadingHdr           ; 着色（SHD）
```

那么就自定义了一个新的热键：Ctrl+Shift+Alt+S，用于执行着色（SHD）命令。