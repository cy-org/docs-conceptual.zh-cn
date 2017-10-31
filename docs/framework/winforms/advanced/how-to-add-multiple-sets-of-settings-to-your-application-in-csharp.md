---
title: "如何：向应用程序添加多个设置组 (C#) | Microsoft Docs"
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
  - "应用程序设置 [Windows 窗体], C#"
  - "应用程序设置 [Windows 窗体], 多个组"
ms.assetid: 45007ac6-cf07-4be7-bc38-3f0ef962faf9
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：向应用程序添加多个设置组 (C#)
在某些情况下，您可能需要在一个应用程序中包含多个设置组。  例如，如果您开发的应用程序中有一个特定的设置组预计会经常更改，则最好是将所有这些设置放入到一个单独的文件中，这样就可以替换整个文件，从而使其他设置不受影响。  Visual Studio 允许您向项目中添加多个设置组。  可以通过 Properties.Settings 对象访问其他设置组。  
  
### 向应用程序添加其他设置组  
  
1.  从**“项目”**菜单中选择**“添加新项”**。  **“添加新项”**对话框打开。  
  
2.  在**“添加新项”**对话框中，选择**“设置文件”**，键入该文件的名称，然后单击**“添加”**以向解决方案中添加新的设置文件。  
  
3.  在**“解决方案资源管理器”**中，将新的设置文件拖动到**“属性”**文件夹中。  这样就可以在代码中使用新设置。  
  
4.  像在任何其他设置文件中一样，在此文件中添加和使用设置。  可以通过 Properties.Settings 对象访问此设置组。  
  
## 请参阅  
 [使用应用程序设置和用户设置](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)