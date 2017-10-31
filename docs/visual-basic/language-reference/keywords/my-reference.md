---
title: "My 引用 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My 功能"
  - "My 引用"
ms.assetid: 6f803bd7-21ff-4569-b1fe-b00a6678b1e3
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# My 引用 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`My` 功能允许您直观的访问常用方法、属性和事件，从而提高了编程的速度和简易性。  本表列出了 `My` 中包含的对象，以及每个对象可执行的操作。  
  
|**操作**|**对象**|  
|------------|------------|  
|访问应用程序信息和服务。|`My.Application` 对象由以下类组成：<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> 提供在所有项目中可用的成员。<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 提供在 Windows 窗体应用程序中可用的成员。<br /><br /> <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> 提供在控制台应用程序中可用的成员。|  
|访问主机及其资源、服务和数据。|`My.Computer` \(<xref:Microsoft.VisualBasic.Devices.Computer>\)|  
|访问当前项目中的窗体。|[My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)|  
|访问 Application 日志。|`My.Application.Log` \(<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.Log%2A>\)|  
|访问当前 Web 请求。|[My.Request 对象](../../../visual-basic/language-reference/objects/my-request-object.md)|  
|访问资源元素。|[My.Resources 对象](../../../visual-basic/language-reference/objects/my-resources-object.md)|  
|访问当前 Web 响应。|[My.Response 对象](../../../visual-basic/language-reference/objects/my-response-object.md)|  
|访问用户和应用程序级设置。|[My.Settings 对象](../../../visual-basic/language-reference/objects/my-settings-object.md)|  
|访问当前用户的安全性上下文。|`My.User` \(<xref:Microsoft.VisualBasic.ApplicationServices.User>\)|  
|访问由当前项目引用的 XML Web services。|[My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)|  
  
## 请参阅  
 [Visual Basic 应用程序模型概述](../../../visual-basic/developing-apps/development-with-my/overview-of-the-visual-basic-application-model.md)   
 [使用 My 开发](../../../visual-basic/developing-apps/development-with-my/index.md)