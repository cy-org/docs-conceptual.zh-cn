---
title: "如何：在应用程序会话之间更改设置值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "应用程序设置 [Windows 窗体], 应用程序会话之间"
  - "应用程序设置 [Windows 窗体], 更改"
ms.assetid: 1a85911f-97b2-476c-930b-83379edd890c
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在应用程序会话之间更改设置值
有时，在编译并部署应用程序之后，您可能需要在应用程序会话之间更改设置值。  例如，可能需要更改指向正确的数据库位置的连接字符串。  由于设计时工具在编译并部署应用程序之后不可用，因此必须手动更改文件中的设置值。  
  
### 在应用程序会话之间更改设置值  
  
1.  使用 Microsoft 记事本或一些其他的文本或 XML 编辑器，打开与应用程序关联的 .config 文件。  
  
2.  定位要更改的设置的项。  该项看起来与下面显示的示例类似。  
  
    ```  
    <setting name="Setting1" serializeAs="String" >  
       <value>My Setting Value</value>  
    </setting>  
    ```  
  
3.  为设置键入新值并保存文件。  
  
## 请参阅  
 [使用应用程序设置和用户设置](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)