---
title: "使用 My.Application、My.Computer 和 My.User 执行任务 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Application 对象, 开发应用程序"
  - "My.Computer 对象, 开发应用程序"
  - "My.User 对象, 开发应用程序"
  - "快速应用程序开发 (RAD), My.Application"
  - "快速应用程序开发 (RAD), My.Computer"
  - "快速应用程序开发 (RAD), My.User"
ms.assetid: c8af61bd-4dd3-4a0f-9af5-795b594b240b
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 使用 My.Application、My.Computer 和 My.User 执行任务 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

三个主要的 `My` 对象为 `My.Application` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>\)、`My.Computer` \(<xref:Microsoft.VisualBasic.Devices.Computer>\) 和 `My.User` \(<xref:Microsoft.VisualBasic.ApplicationServices.User>\)，它们提供对信息和常用功能的访问。  通过使用这些对象，您可以分别访问与当前应用程序、安装该应用程序的计算机或该应用程序的当前用户相关的信息。  
  
## My.Application、My.Computer 和 My.User  
 下面的示例演示如何使用 `My` 检索信息。  
  
 [!code-vb[VbVbcnMy#1](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_1.vb)]  
  
 [!code-vb[VbVbcnMy#2](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_2.vb)]  
  
 除检索信息外，通过这三个对象公开的成员还允许您执行与该对象相关的方法。  例如，您可以访问多种方法来操作文件，或者通过 `My.Computer` 更新注册表。  
  
 由于 `My` 中包含大量用于操作文件、目录和驱动器的方法和属性，因此借助此对象，文件 I\/O 将变得非常简单快捷。  通过 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> 对象，可以从具有分隔字段或固定宽度字段的大结构化文件中读取数据。  此示例打开 `TextFieldParser` `reader`，然后使用它读取 `C:\TestFolder1\test1.txt` 中的数据。  
  
 [!code-vb[VbVbalrTextFieldParser#23](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_3.vb)]  
  
 通过 `My.Application` 可以更改应用程序的区域性。  下面的示例演示如何能调用此方法。  
  
 [!code-vb[VbVbcnMy#3](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/performing-tasks-with-my-application-my-computer-and-my-user_4.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [My 对项目类型的依赖方式](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)