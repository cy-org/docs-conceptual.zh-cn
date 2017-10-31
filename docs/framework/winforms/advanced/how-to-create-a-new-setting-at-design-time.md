---
title: "如何：在设计时创建新设置 | Microsoft Docs"
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
  - "应用程序设置 [Windows 窗体], 创建"
  - "应用程序设置 [Windows 窗体], 设计时"
ms.assetid: c5d60a66-6507-462f-a81f-e3bc0a804e16
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在设计时创建新设置
通过使用设置设计器，可以在运行时创建新设置。  设置设计器是一个网格样式的界面，它允许您创建新设置并指定这些设置的属性。  必须为新设置指定名称、值、类型和范围。  一旦创建某个设置，就可以使用代码访问它。  
  
### 在设计时创建新设置 \(C\#\)  
  
1.  在**“解决方案资源管理器”**中，展开项目的**“属性”**节点。  
  
2.  双击要在其中添加新设置的 .settings 文件。  此文件的默认名称为 Settings.settings。  
  
3.  在设置设计器中，设置您的设置的名称、值、类型和范围。  每一行代表一个设置。  
  
### 在设计时创建新设置 \(Visual Basic\)  
  
1.  在**“解决方案资源管理器”**中，右击项目节点并选择**“属性”**。  
  
2.  在**“属性”**页中，选择**“设置”**选项卡。  
  
3.  在设置设计器中，设置您的设置的名称、值、类型和范围。  每一行代表一个设置。  
  
## 请参阅  
 [使用应用程序设置和用户设置](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [如何：在设计时更改现有设置的值](../../../../docs/framework/winforms/advanced/how-to-change-the-value-of-an-existing-setting-at-design-time.md)