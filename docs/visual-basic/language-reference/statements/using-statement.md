---
title: "Using 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.using"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "资源处置"
  - "资源 [Visual Basic], 释放"
  - "Try...Catch...Finally 语句, 等效于 Using 语句"
  - "Using 语句"
ms.assetid: 665d1580-dd54-4e96-a9a9-6be2a68948f1
caps.latest.revision: 36
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 36
---
# Using 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明 `Using` 块的开头，并根据需要获取该块控制的系统资源。  
  
## 语法  
  
```  
Using { resourcelist | resourceexpression }  
    [ statements ]  
End Using  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`resourcelist`|如果未提供 `resourceexpression`，则是必选项。  列出一个或多个系统资源此 `Using` 个控件，以逗号分隔。|  
|`resourceexpression`|如果未提供 `resourcelist`，则是必选项。  引用要由此 `Using` 块控制的某个系统资源的引用变量或表达式。|  
|`statements`|可选。  `Using` 块运行的语句块。|  
|`End Using`|必需。  终止 `Using` 块的定义，并释放该块控制的所有资源。|  
  
 `resourcelist` 部分中的每个资源都具有以下语法和组成部分：  
  
 `resourcename As New resourcetype [ ( [ arglist ] ) ]`  
  
 \- 或 \-  
  
 `resourcename As resourcetype = resourceexpression`  
  
## resourcelist 部分  
  
|||  
|-|-|  
|术语|定义|  
|`resourcename`|必需。  引用 `Using` 块控制的系统资源的引用变量。|  
|`New`|如果 `Using` 语句获取资源，则为必选项。  如果已获取了资源，请使用第二种备选语法。|  
|`resourcetype`|必需。  资源的类。  该类必须实现 <xref:System.IDisposable> 接口。|  
|`arglist`|可选。  您为创建 `resourcetype` 实例而传递到构造函数的参数的列表。  请参见 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。|  
|`resourceexpression`|必需。  引用符合 `resourcetype` 要求的系统资源的变量或表达式。  如果使用第二种备选语法，那么，在将控制传递给 `Using` 语句之前，您必须获取资源。|  
  
## 备注  
 有时，代码要求非托管资源，如文件句柄、COM 包装或 SQL 连接。  在使用一个或多个此类资源完成了代码后，`Using` 块确保这些资源的释放。  这样，其他代码就可以使用它们。  
  
 托管资源由 .NET Framework 垃圾回收器 \(GC\) 释放，您不需要进行任何额外的编码。  您也不需要用于托管资源的 `Using` 块。  但是，仍可以使用 `Using` 块强制释放托管的资源，而不是等待垃圾回收器处理。  
  
 `Using` 块有三个部分：获取、使用和释放。  
  
-   获取表示创建变量并将其初始化，以便引用系统资源。  `Using` 语句可获取一个或多个资源，您可以在进入块之前恰好获取一个资源，并将其提供给 `Using` 语句。  如果提供 `resourceexpression`，在将控制权传递给 `Using` 语句之前，您必须获取资源。  
  
-   使用表示访问资源并使用资源执行操作。  `Using` 和 `End Using` 之间的语句代表资源的使用过程。  
  
-   释放表示针对 `resourcename` 中的对象调用 <xref:System.IDisposable.Dispose%2A> 方法。  这使该对象可以明确终止其资源。  `End Using` 语句释放 `Using` 块控制的资源。  
  
## 行为  
 `Using` 块的工作方式类似于 `Try`...`Finally` 构造，在该构造中，`Try` 块使用资源，而 `Finally` 块释放资源。  因此，不管您如何退出块，`Using` 块都可确保资源的释放。  即使发生未经处理的异常（除 <xref:System.StackOverflowException> 外），也是如此。  
  
 `Using` 语句获取的每个资源变量的范围仅限于 `Using` 块。  
  
 如果在 `Using` 语句中指定多个系统资源，效果就好像您将多个 `Using` 块相互嵌套一样。  
  
 如果 `resourcename` 是 `Nothing`，不调用 <xref:System.IDisposable.Dispose%2A> 进行，因此，不会引发异常。  
  
## Using 块中的结构化异常处理  
 如果需要处理可能发生在 `Using` 块中的异常，可以向该块中添加一个完整的 `Try`...`Finally` 构造。  如果需要处理 `Using` 语句未成功获取资源的情况，可以进行测试，以确定 `resourcename` 是否为 `Nothing`。  
  
## 进行结构化异常处理而不使用 Using 块  
 如果需要对资源的获取进行更细致的控制，或者需要 `Finally` 块中的附加代码，可以将 `Using` 块重写为 `Try`...`Finally` 构造。  下面的示例显示主干 `Try` 和 `Using` 构造，这两个构造在获取和释放 `resource` 过程中是等效的。  
  
```vb  
Using resource As New resourceType   
    ' Insert code to work with resource.  
End Using  
  
' For the acquisition and disposal of resource, the following  
' Try construction is equivalent to the Using block.  
Dim resource As New resourceType  
Try   
    ' Insert code to work with resource.  
Finally   
    If resource IsNot Nothing Then  
        resource.Dispose()   
    End If  
End Try   
```  
  
> [!NOTE]
>  `Using` 块内部的代码不应将 `resourcename` 中的对象赋给其他变量。  当您退出 `Using` 块时，资源将被释放，于是其他变量将无法访问它所指向的资源。  
  
## 示例  
 下面的示例创建名为 log.txt 和写入文本两行对文件的文件。  此示例读取同一文件并显示文本行。  
  
 由于 <xref:System.IO.TextWriter> 和 <xref:System.IO.TextReader> 选件类实现 <xref:System.IDisposable> 接口，代码可以使用 `Using` 语句来确保文件在读写操作之后正常关闭。  
  
 [!code-vb[VbVbalrStatements#50](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/using-statement_1.vb)]  
  
## 请参阅  
 <xref:System.IDisposable>   
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [如何：释放系统资源](../../../visual-basic/programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md)