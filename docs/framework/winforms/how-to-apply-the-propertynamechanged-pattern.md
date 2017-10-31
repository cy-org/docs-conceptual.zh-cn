---
title: "如何：应用 PropertyNameChanged 模式 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 属性更改（使用代码）"
  - "数据绑定, 自定义控件"
  - "PropertyNameChanged , 应用"
ms.assetid: aa47ddf6-5223-40c4-833f-a78992194836
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：应用 PropertyNameChanged 模式
下面的代码示例演示如何将*属性名称*Changed 模式应用于自定义控件。  在实现与 Windows 窗体数据绑定引擎一起使用的自定义控件时，请应用此模式。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.ChangeNotification#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ChangeNotification/CS/Form1.cs#3)]
 [!code-vb[System.Windows.Forms.ChangeNotification#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ChangeNotification/VB/Form1.vb#3)]  
  
## 编译代码  
 若要编译上面的代码示例：  
  
-   将该代码粘贴到空白代码文件中。  您必须在包含 `Main` 方法的 Windows 窗体上使用该自定义控件。  
  
## 请参阅  
 [如何：实现 INotifyPropertyChanged 接口](../../../docs/framework/winforms/how-to-implement-the-inotifypropertychanged-interface.md)   
 [Windows 窗体数据绑定中的更改通知](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)