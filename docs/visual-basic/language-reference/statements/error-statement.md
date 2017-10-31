---
title: "Error 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.error"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Error 关键字"
  - "Error 语句"
  - "Error 语句, 语法"
  - "错误 [Visual Basic], 模拟"
  - "运行时错误, 代码"
ms.assetid: 85cd5c59-5224-4f02-aaf5-fcfefab17a29
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Error 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

模拟错误的发生。  
  
## 语法  
  
```  
Error errornumber  
```  
  
## 部件  
 `errornumber`  
 必选。  可以是任何有效错误号。  
  
## 备注  
 `Error` 语句支持向后兼容。  在新代码中，特别是创建对象时，请使用 `Err` 对象的 `Raise` 方法来生成运行时错误。  
  
 如果 `errornumber` 已经定义，则在 `Err` 对象的属性设置为如下默认值后，`Error` 语句会调用错误处理程序：  
  
|属性|值|  
|--------|-------|  
|`Number`|指定作为 `Error` 语句参数的值。  可以是任何有效错误号。|  
|`Source`|当前 Visual Basic 项目的名称。|  
|`Description`|与 `Error` 函数为指定的 `Number` 返回的值对应的字符串表达式（如果该字符串存在）。  如果不存在字符串，`Description` 为一个零长度字符串 \(""\)。|  
|`HelpFile`|相应 Visual Basic 帮助文件的完全限定的驱动器、路径和文件名。|  
|`HelpContext`|与 `Number` 属性对应的错误的相应 Visual Basic 帮助文件上下文 ID。|  
|`LastDLLError`|零。|  
  
 如果没有错误处理程序，或者错误处理程序未启用，会创建错误消息并从 `Err` 对象属性显示。  
  
> [!NOTE]
>  有些 Visual Basic 宿主应用程序无法创建对象。  请参见您的宿主应用程序的文档，确定其是否可以创建类和对象。  
  
## 示例  
 此示例使用 `Error` 语句生成错误号 11。  
  
```  
On Error Resume Next   ' Defer error handling.  
Error 11   ' Simulate the "Division by zero" error.  
```  
  
## 要求  
 **命名空间：** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **程序集：**Visual Basic 运行库（位于 Microsoft.VisualBasic.dll 中）  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ErrObject.Clear%2A>   
 <xref:Microsoft.VisualBasic.Information.Err%2A>   
 <xref:Microsoft.VisualBasic.ErrObject.Raise%2A>   
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)   
 [Resume 语句](../../../visual-basic/language-reference/statements/resume-statement.md)   
 [错误消息](../../../visual-basic/language-reference/error-messages/index.md)