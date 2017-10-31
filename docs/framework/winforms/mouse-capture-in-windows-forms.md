---
title: "Windows 窗体中的鼠标捕获 | Microsoft Docs"
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
  - "鼠标, 捕获"
ms.assetid: 8911d4b0-a4f8-4f93-8246-371aebd27d0c
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Windows 窗体中的鼠标捕获
“鼠标捕获”指控件何时执行所有鼠标输入的命令。  控件捕获鼠标后，不论鼠标指针是否在控件的边框内，该控件都接收鼠标输入。  
  
## 设置鼠标捕获  
 在 Windows 窗体中，当用户在某个控件上按下鼠标按钮时，该控件便捕获鼠标，当用户释放鼠标按钮时，该控件便释放鼠标。  
  
 <xref:System.Windows.Forms.Control> 类的 <xref:System.Windows.Forms.Control.Capture%2A> 属性指定控件是否已捕获鼠标。  若要确定控件何时失去鼠标捕获，需处理 <xref:System.Windows.Forms.Control.MouseCaptureChanged> 事件。  
  
 只有前台窗口可以捕获鼠标。  当后台窗口尝试捕获鼠标时，只有鼠标指针位于该窗口可见部分时，该窗口才接收所发生的鼠标事件的信息。  另外，即使前台窗口已捕获鼠标，用户仍可以单击另一个窗口，从而使后者成为前台窗口。  捕获鼠标时，快捷键无效。  
  
## 请参阅  
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)