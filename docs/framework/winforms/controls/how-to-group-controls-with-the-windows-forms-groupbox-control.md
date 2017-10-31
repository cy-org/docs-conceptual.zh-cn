---
title: "如何：使用 Windows 窗体 GroupBox 控件对控件分组 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体], 分组"
  - "GroupBox 控件 [Windows 窗体], 将控件分组"
  - "Windows 窗体控件, 分组"
ms.assetid: 0bda316d-bd2a-43aa-ac73-342453303169
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用 Windows 窗体 GroupBox 控件对控件分组
Windows 窗体 <xref:System.Windows.Forms.GroupBox> 控件用于对其他控件进行分组。  对控件分组的原因有三个：  
  
-   对相关窗体元素进行可视化分组以构造一个清晰的用户界面。  
  
-   创建编程分组（例如，单选按钮分组）。  
  
-   设计时将多个控件作为一个单元移动。  
  
### 创建一组控件  
  
1.  在窗体上绘制 <xref:System.Windows.Forms.GroupBox> 控件。  
  
2.  向分组框添加其他控件，在分组框内绘制各个控件。  
  
     如果要将现有控件放到分组框中，可以选定所有这些控件，将它们剪切到剪贴板，选择 <xref:System.Windows.Forms.GroupBox> 控件，再将它们粘贴到分组框中。  也可以将它们拖到分组框中。  
  
3.  将分组框的 <xref:System.Windows.Forms.GroupBox.Text%2A> 属性设置为适当标题。  
  
## 请参阅  
 <xref:System.Windows.Forms.GroupBox>   
 [GroupBox 控件](../../../../docs/framework/winforms/controls/groupbox-control-windows-forms.md)