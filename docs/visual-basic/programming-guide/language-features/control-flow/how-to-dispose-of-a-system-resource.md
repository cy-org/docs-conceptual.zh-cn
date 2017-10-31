---
title: "如何：释放系统资源 (Visual Basic) | Microsoft Docs"
ms.custom: ""
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
  - "资源 [Visual Basic], 释放系统"
  - "系统资源"
  - "系统资源, 释放"
  - "Using 块"
  - "Using 语句, 释放系统资源"
  - "Using 语句, Using...End Using"
  - "Visual Basic 代码, 控制流"
ms.assetid: 8be2b239-8090-419b-8e7e-bcaa75b0ecc8
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：释放系统资源 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以使用 `Using` 块保证系统在代码退出该块时释放资源。  如果正在使用消耗大量内存或其他组件也需要使用的系统资源时，这样处理十分有用。  
  
### 代码完成数据库连接时释放数据库连接  
  
1.  确保在源文件的开始包含该数据库连接的适当 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)（本例中为 <xref:System.Data.SqlClient>）。  
  
2.  创建具有 `Using` 和 `End Using` 语句的 `Using` 块。  在块中放入处理数据库连接的代码。  
  
3.  声明连接并创建其实例作为 `Using` 语句的一部分。  
  
    ```  
    ' Insert the following line at the beginning of your source file.  
    Imports System.Data.SqlClient  
    Public Sub AccessSql(ByVal s As String)  
        Using sqc As New System.Data.SqlClient.SqlConnection(s)  
            MsgBox("Connected with string """ & sqc.ConnectionString & """")  
        End Using  
    End Sub  
    ```  
  
     无论退出块的方式如何（包括未经处理的异常的情况），系统都会释放该资源。  
  
     注意：不能从 `Using` 块外部访问 `sqc`，这是因为其范围只限于该块。  
  
     对系统资源（如文件句柄或 COM 包装）可以使用同样的方法。  如果要确保退出 `Using` 块后其他组件还能使用资源，则可使用 `Using` 块。  
  
## 请参阅  
 <xref:System.Data.SqlClient.SqlConnection>   
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [决策结构](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [其他控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)   
 [嵌套的控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)