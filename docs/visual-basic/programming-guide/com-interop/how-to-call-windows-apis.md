---
title: "如何：调用 Windows API (Visual Basic) | Microsoft Docs"
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
  - "API 调用"
  - "API 调用, 平台调用"
  - "调用, 存储过程"
  - "Windows API, 调用"
ms.assetid: 27d75f0a-54ab-4ee1-b91d-43513a19b12d
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：调用 Windows API (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此示例定义和调用 user32.dll 中的函数 `MessageBox` 然后将一个字符串传递给它。  
  
## 示例  
 [!code-vb[VbVbalrInterop#1](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/how-to-call-windows-apis_1.vb)]  
  
## 编译代码  
 此示例需要:  
  
-   为 <xref:System> 命名空间的引用。  
  
## 可靠编程  
 以下情况可能会导致异常:  
  
-   该方法不是静态的，是抽象的或者以前已定义。  父类型为接口，或者 *名称* 或 *dllName* 的长度为零。  \(<xref:System.ArgumentException>\)  
  
-   *名称* 或 *dllName* 是 `Nothing`。  \(<xref:System.ArgumentNullException>\)  
  
-   使用 `CreateType`，包含的类型以前创建的。  \(<xref:System.InvalidOperationException>\)  
  
## 请参阅  
 [A Closer Look at Platform Invoke](http://msdn.microsoft.com/zh-cn/ba9dd55b-2eaa-45cd-8afd-75cb8d64d243)   
 [平台调用示例](../Topic/Platform%20Invoke%20Examples.md)   
 [使用非托管 DLL 函数](../Topic/Consuming%20Unmanaged%20DLL%20Functions.md)   
 [Defining a Method with Reflection Emit](http://msdn.microsoft.com/zh-cn/84fd3bf6-628f-41aa-83d9-b990cf926e81)   
 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)   
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)