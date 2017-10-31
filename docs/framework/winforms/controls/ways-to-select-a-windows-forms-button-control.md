---
title: "选择 Windows 窗体 Button 控件的方法 | Microsoft Docs"
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
  - "Button 控件 [Windows 窗体], 选择"
ms.assetid: fe2fc058-5118-4f70-b264-6147d64a7a8d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 选择 Windows 窗体 Button 控件的方法
可以用下列方法选择 Windows 窗体按钮：  
  
-   使用鼠标单击该按钮。  
  
-   在代码中调用该按钮的 <xref:System.Windows.Forms.Control.Click> 事件。  
  
-   通过按 Tab 键将焦点移动到该按钮上，然后按空格键或 Enter 选择该按钮。  
  
-   按该按钮的访问键（Alt \+ 带有下划线的字母）。  有关访问键的更多信息，请参见 [如何：创建 Windows 窗体控件的访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md)。  
  
-   如果该按钮是窗体的“接受”按钮，那么即使另一个控件具有焦点（但该控件不可以是另一个按钮、多行文本框或捕获 Enter 键的自定义控件），按 Enter 也将选择该按钮。  
  
-   如果该按钮是窗体的“取消”按钮，那么即使另一个控件具有焦点，按 Esc 也将选择该按钮。  
  
-   调用 <xref:System.Windows.Forms.Button.PerformClick%2A> 方法以编程方式选择该按钮。  
  
## 请参阅  
 [Button 控件概述](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)   
 [如何：响应 Windows 窗体按钮的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)   
 [Button 控件](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)