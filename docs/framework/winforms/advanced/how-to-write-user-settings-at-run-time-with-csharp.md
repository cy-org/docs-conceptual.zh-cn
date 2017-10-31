---
title: "如何：在运行时编写用户设置 (C#) | Microsoft Docs"
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
  - "应用程序设置 [Windows 窗体], 运行时"
  - "应用程序设置 [Windows 窗体], 写入用户设置"
ms.assetid: 9d061c7d-b33b-470f-a36d-edccb1d6f9a3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：在运行时编写用户设置 (C#)
应用程序范围的设置是只读的，只能在设计时更改，或通过在应用程序会话之间更改 .config 文件进行更改。  但用户范围的设置可以在运行时写入，就像更改任何属性值一样。  新值在应用程序会话的持续时间内始终存在。  可以通过调用 Save 方法在应用程序会话之间保留对设置的更改。  
  
### 如何：在运行时编写和保留用户设置 \(C\#\)  
  
1.  访问设置并向其分配新值，如本示例中所示：  
  
    ```  
    // C#  
    Properties.Settings.Default.myColor = Color.AliceBlue;  
    ```  
  
2.  如果想要到在应用程序会话之间保留对设置的更改，请调用 Save 方法，如本示例中所示：  
  
    ```  
    // C#  
    Properties.Settings.Default.Save();  
    ```  
  
     用户设置保存在用户的本地应用程序数据文件夹（隐藏）中子文件夹下的文件内。  
  
## 请参阅  
 [使用应用程序设置和用户设置](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [如何：在运行时读取设置 \(C\#\)](../../../../docs/framework/winforms/advanced/how-to-read-settings-at-run-time-with-csharp.md)   
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)