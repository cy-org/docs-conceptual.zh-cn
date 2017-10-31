---
title: "如何：在运行时读取设置 (C#) | Microsoft Docs"
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
  - "应用程序设置 [Windows 窗体], 读取"
  - "应用程序设置 [Windows 窗体], 运行时"
ms.assetid: dbe8bf09-5e1c-49da-9192-154033d7240b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在运行时读取设置 (C#)
可以通过“属性”对象在运行时读取应用程序范围和用户范围的设置。  “属性”对象通过 Properties.Settings.Default 成员公开项目的所有默认设置。  
  
### 在运行时读取设置 \(C\#\)  
  
-   请通过 Properties.Settings.Default 成员访问相应的设置。  下面的示例演示如何将名为 `myColor` 的设置分配给 BackColor 属性。  这要求你在之前已创建包含名为 `myColor` 的设置（其类型为 `System.Drawing.Color`）的设置文件。  有关创建设置文件的信息，请参阅[如何：在设计时创建新设置](../../../../docs/framework/winforms/advanced/how-to-create-a-new-setting-at-design-time.md)。  
  
    ```  
    // C#  
    this.BackColor = Properties.Settings.Default.myColor;  
    ```  
  
## 请参阅  
 [使用应用程序设置和用户设置](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [如何：在运行时编写用户设置 \(C\#\)](../../../../docs/framework/winforms/advanced/how-to-write-user-settings-at-run-time-with-csharp.md)   
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)