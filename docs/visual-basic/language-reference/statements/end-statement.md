---
title: "End 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.End"
  - "End"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "代码, 退出"
  - "End 关键字, End 语句"
  - "End 语句"
  - "执行, 结束"
  - "执行, stopping"
  - "文件, 关闭"
  - "程序终止"
  - "程序, 退出"
ms.assetid: 0e64467c-0f34-4aab-9ddd-43f8b9d55d90
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# End 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

立即终止执行。  
  
## 语法  
  
```  
End  
```  
  
## 备注  
 可以将 `End` 语句放在过程中任意处，以强制整个应用程序停止运行。  `End` 关闭用 `Open` 语句打开的所有文件，并清除所有应用程序的变量。  只要其他程序没有引用应用程序的对象并且应用程序的代码当前都未运行，该应用程序就会立即关闭。  
  
> [!NOTE]
>  `End` 语句会突然停止代码的执行，而不调用 `Dispose`、`Finalize` 方法或任何其他 Visual Basic 代码。  这将使其他程序所持有的对象引用无效。  如果在 `Try` 或 `Catch` 块中遇到 `End` 语句，控制不会传递到对应的 `Finally` 块。  
  
 `Stop` 语句中止执行，但与 `End` 不同，它不关闭任何文件或清除任何变量，除非在已编译的可执行 \(.exe\) 文件中遇到它。  
  
 由于 `End` 会立即终止应用程序，而不顾及任何可能已打开的资源，因此在使用该语句前，应尝试彻底关闭所有资源。  例如，如果应用程序中还有打开的窗体，应该先关闭这些窗体，然后再将控制传递给 `End` 语句。  
  
 尽量少用 `End`，只有在需要立即停止时才使用该语句。  终止过程的正常方式（[Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 和 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)）不仅彻底关闭过程，而且允许彻底关闭调用代码。  例如，控制台应用程序即可直接从 `Main` 过程 `Return`。  
  
> [!IMPORTANT]
>  `End` 语句调用 <xref:System> 命名空间中的 <xref:System.Environment> 类的 <xref:System.Environment.Exit%2A> 方法。  <xref:System.Environment.Exit%2A> 要求您具有 `UnmanagedCode` 权限。  如果没有该权限，则会出现 <xref:System.Security.SecurityException> 错误。  
  
 当后面跟有附加的关键字时，[End \<关键字\> 语句](../../../visual-basic/language-reference/statements/end-keyword-statement.md) 表明结束对相应过程或块的定义。  例如，`End Function` 终止 `Function` 过程的定义。  
  
## 示例  
 下面的示例使用 `End` 语句终止代码执行（如果用户请求这样做）。  
  
 [!code-vb[VbVersHelp60Controls#64](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/end-statement_1.vb)]  
  
## 智能设备开发人员说明  
 不支持此语句。  
  
## 请参阅  
 <xref:System.Security.Permissions.SecurityPermissionFlag>   
 [Stop 语句](../../../visual-basic/language-reference/statements/stop-statement.md)   
 [End \<关键字\> 语句](../../../visual-basic/language-reference/statements/end-keyword-statement.md)