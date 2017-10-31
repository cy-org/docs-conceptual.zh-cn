---
title: "如何：对 Windows 窗体上的对象分层 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 分层"
  - "控件 [Windows 窗体], 定位"
  - "Windows 窗体控件, 分层"
  - "z 顺序"
  - "z 顺序"
ms.assetid: 1acc4281-2976-4715-86f4-bda68134baaf
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：对 Windows 窗体上的对象分层
当创建复杂用户界面或使用多文档界面 \(MDI\) 窗体时，经常需要将控件和子窗体分层，以便创建更复杂的用户界面 \(UI\)。  若要在组的上下文内移动和跟踪控件和窗口，可操作其 Z 顺序。  Z 顺序是窗体上的控件沿窗体的 Z 轴（深度）方向的可视化分层。  位于 Z 顺序顶层的窗口重叠在所有其他窗口之上。  所有其他窗口重叠在 Z 顺序底部的窗口之上。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时将控件分层  
  
1.  选择要分层的控件。  
  
2.  在**“格式”**菜单上，指向**“顺序”**，然后单击**“置于顶层”**或**“置于底层”**。  
  
### 以编程方式将控件分层  
  
-   使用 <xref:System.Windows.Forms.Control.BringToFront%2A> 和 <xref:System.Windows.Forms.Control.SendToBack%2A> 方法操作控件的 Z 顺序。  
  
     例如，如果 <xref:System.Windows.Forms.TextBox> 控件 `txtFirstName` 位于另一个控件的下面，而您希望将其放在顶层，请使用下列代码：  
  
    ```vb  
    txtFirstName.BringToFront()  
  
    ```  
  
    ```csharp  
    txtFirstName.BringToFront();  
  
    ```  
  
    ```cpp  
    txtFirstName->BringToFront();  
    ```  
  
> [!NOTE]
>  Windows 窗体支持*控件包容*。  控件包容是指将多个控件放在一个包容控件内，如将多个 <xref:System.Windows.Forms.RadioButton> 控件放在 <xref:System.Windows.Forms.GroupBox> 控件内。  然后可在包容控件内将控件分层。  由于控件包含在分组框内，所以移动分组框也会移动这些控件。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)