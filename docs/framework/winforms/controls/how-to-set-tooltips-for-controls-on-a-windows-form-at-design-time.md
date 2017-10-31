---
title: "如何：在设计时为 Windows 窗体上的控件设置工具提示 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 工具提示"
  - "工具提示 [Windows 窗体], 对于控件"
ms.assetid: c4b60637-4c0a-44c2-a103-f66dff887936
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：在设计时为 Windows 窗体上的控件设置工具提示
可在代码中或 Windows 窗体设计器中设置 <xref:System.Windows.Forms.ToolTip> 字符串。  有关 <xref:System.Windows.Forms.ToolTip> 组件的更多信息，请参见 [ToolTip 组件概述](../../../../docs/framework/winforms/controls/tooltip-component-overview-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 以编程方式设置工具提示  
  
1.  添加将显示工具提示的控件。  
  
2.  使用 <xref:System.Windows.Forms.ToolTip> 组件的 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 方法。  
  
    ```vb  
    ' In this example, Button1 is the control to display the ToolTip.  
    ToolTip1.SetToolTip(Button1, "Save changes")  
  
    ```  
  
    ```csharp  
    // In this example, button1 is the control to display the ToolTip.  
    toolTip1.SetToolTip(button1, "Save changes");  
  
    ```  
  
    ```cpp  
    // In this example, button1 is the control to display the ToolTip.  
    toolTip1->SetToolTip(button1, "Save changes");  
    ```  
  
### 在设计器中设置工具提示  
  
1.  将一个 <xref:System.Windows.Forms.ToolTip> 组件添加到窗体中。  
  
2.  选择将显示工具提示的控件，或将其添加到窗体。  
  
3.  在**“属性”**窗口中将**“ToolTip1 上的 ToolTip”**值设置为适当的文本字符串。  
  
## 请参阅  
 [ToolTip 组件概述](../../../../docs/framework/winforms/controls/tooltip-component-overview-windows-forms.md)   
 [如何：更改 Windows 窗体 ToolTip 组件的延迟](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)   
 [ToolTip 组件](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md)