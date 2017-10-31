---
title: "支持辅助功能准则的 Windows 窗体控件上的属性 | Microsoft Docs"
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
  - "辅助功能, Windows 窗体控件属性"
  - "Windows 窗体, 控件的辅助功能属性"
ms.assetid: ad3567a6-313b-4708-9e15-f487a831f049
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 支持辅助功能准则的 Windows 窗体控件上的属性
“Windows 窗体”标准工具箱上的控件支持许多辅助功能准则，包括公开键盘焦点和屏幕元素。  
  
## 预先规划辅助功能  
 控件的属性可用于支持其他辅助功能准则，如下表所示。  另外，应该使用菜单提供对程序功能的访问权。  
  
|控件属性|辅助功能注意事项|  
|----------|--------------|  
|AccessibleDescription|此描述报告给辅助功能（如屏幕读取器）。  辅助功能是一些专用的程序和设备，用于帮助残疾人更有效地使用计算机。|  
|AccessibleName|报告给辅助功能的名称。|  
|AccessibleRole|描述用户界面中元素的用途。|  
|TabIndex|创建一个在窗体中导航的合理路径。  没有内部标签的控件（如文本框）必须按 Tab 键顺序紧跟在其关联标签之后，这非常重要。|  
|Text|使用“&”字符创建访问键。  使用访问键是提供对功能的已记录的键盘访问方案的一部分。|  
|Font Size|如字体大小是不可调整的，则应当将它设为 10 磅或更大。  一旦设置了窗体的字体大小，所有以后添加到窗体的控件的字体将具有相同大小。|  
|Forecolor|如果该属性设置为默认值，则将在窗体上使用用户的颜色首选项。|  
|Backcolor|如果该属性设置为默认值，则将在窗体上使用用户的颜色首选项。|  
|BackgroundImage|将此属性保留为空以使文本更可读。|  
  
## 请参阅  
 [演练：创建可访问的基于 Windows 的应用程序](../../../../docs/framework/winforms/advanced/walkthrough-creating-an-accessible-windows-based-application.md)