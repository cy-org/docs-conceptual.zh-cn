---
title: "@（指定响应文件）(Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "@（指定响应文件）编译器选项 [Visual Basic]"
ms.assetid: a6847eaa-e5f9-4303-9421-45b55484b9ca
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# @（指定响应文件）(Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个文件，该文件包含编译器选项和要编译的源代码文件。  
  
## 语法  
  
```  
@response_file  
```  
  
## 参数  
 `response_file`  
 必选。  一个列出编译器选项或要编译的源代码文件的文件。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。  
  
## 备注  
 编译器处理响应文件中指定的编译器选项和源代码文件，如同它们是在命令行上指定的一样。  
  
 若要在一次编译中指定多个响应文件，请指定如下所示的多个响应文件选项。  
  
```  
@file1.rsp @file2.rsp  
```  
  
 在响应文件中，多个编译器选项和源代码文件可以出现在同一行中。  单个编译器选项的指定必须出现在同一行中（不能跨行）。  响应文件可以带有以 `#` 符号开始的注释。  
  
 可以将在命令行指定的选项同在一个或多个响应文件中指定的选项组合使用。  编译器在遇到命令选项时对其进行处理。  因此，命令行参数可以重写先前在响应文件中列出的选项。  反之，响应文件中的选项将重写先前在命令行或其他响应文件中列出的选项。  
  
 Visual Basic 提供 Vbc.rsp 文件，该文件与 Vbc.exe 文件位于同一目录中。  如果没有使用 `/noconfig` 选项，默认情况下将包括 Vbc.rsp 文件。  有关更多信息，请参见 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)。  
  
> [!NOTE]
>  `@` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 示例  
 下面的代码行来自示例响应文件。  
  
```  
# build the first output file  
/target:exe   
/out:MyExe.exe  
source1.vb   
source2.vb  
```  
  
## 示例  
 下面的示例演示在名为 `File1.rsp` 的响应文件中如何使用 `@` 选项。  
  
```  
vbc @file1.rsp  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)