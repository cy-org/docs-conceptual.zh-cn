---
title: "How to: Prevent a Child Task from Attaching to its Parent | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tasks, preventing attachments"
ms.assetid: c0fb85d4-9e80-4905-9f65-29acc54201c4
caps.latest.revision: 5
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# How to: Prevent a Child Task from Attaching to its Parent
本文档演示如何阻止子任务附加到父任务。  在调用由第三方编写的也使用任务的组件时，阻止子任务附加到其父级是有用的。  例如，使用 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项创建 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 对象的第三方组件可能导致代码中出现问题，如果长时间运行或引发未经处理的异常。  
  
## 示例  
 下面的示例比较使用默认选项和阻止子任务附加到父任务的效果。  示例创建可调入第三方库同时也使用 <xref:System.Threading.Tasks.Task> 对象的 <xref:System.Threading.Tasks.Task> 对象。  第三方库使用 <xref:System.Threading.Tasks.TaskCreationOptions> 选项创建 <xref:System.Threading.Tasks.Task> 对象。  应用程序使用 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项创建父任务。  该选项指示运行时移除的子任务中的 <xref:System.Threading.Tasks.TaskCreationOptions> 规范。  
  
 [!code-csharp[TPL_DenyChildAttach#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_denychildattach/cs/denychildattach.cs#1)]
 [!code-vb[TPL_DenyChildAttach#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_denychildattach/vb/denychildattach.vb#1)]  
  
 因为父任务只有在所有子任务完成后才会完成，所以长时间运行的子任务会让整个应用程序执行得非常缓慢。  在此示例中，当应用程序使用默认选项创建父任务时，子任务必须在父任务完成之前完成。  当应用程序使用 <xref:System.Threading.Tasks.TaskCreationOptions?displayProperty=fullName> 选项时，子任务不会附加到父任务。  因此，应用程序可以在父任务完成之后而必须等待子任务完成之前执行额外工作。  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `DenyChildAttach.cs` \(`DenyChildAttach.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe DenyChildAttach.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe DenyChildAttach.vb**  
  
## 可靠编程  
  
## 请参阅  
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)