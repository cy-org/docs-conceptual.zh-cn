---
title: "如何：在 Windows 窗体上定位控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Location"
  - "Location.Y"
  - "Location.X"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体]"
  - "控件 [Windows 窗体], 移动"
  - "控件 [Windows 窗体], 定位"
  - "对齐线"
ms.assetid: 4693977e-34a4-4f19-8221-68c3120c2b2b
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：在 Windows 窗体上定位控件
若要定位控件，请使用 Windows 窗体设计器，或指定 <xref:System.Windows.Forms.Control.Location%2A> 属性。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在 Windows 窗体设计器的设计图面上定位控件  
  
-   用鼠标将控件拖动到适当位置。  
  
    > [!NOTE]
    >  选中该控件并使用箭头键移动它，以便更精确地定位。  另外，“对齐线”可以帮助您在窗体上精确地放置控件。  有关更多信息，请参见[演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)。  
  
### 使用“属性”窗口定位控件  
  
1.  单击要定位的控件。  
  
2.  在**“属性”**窗口中，键入 <xref:System.Windows.Forms.Control.Location%2A> 属性的值（用逗号分隔），以便在控件的容器内定位该控件。  
  
     第一个数字 \(X\) 是到容器左边界的距离，第二个数字 \(Y\) 是到容器区域上边界的距离，这些数字以像素为单位。  
  
    > [!NOTE]
    >  可以展开 <xref:System.Windows.Forms.Control.Location%2A> 属性以分别键入**“X”**和**“Y”**值。  
  
### 以编程方式定位控件  
  
1.  将该控件的 <xref:System.Windows.Forms.Control.Location%2A> 属性设置为一个 <xref:System.Drawing.Point>。  
  
    ```vb  
    Button1.Location = New Point(100, 100)  
    ```  
  
    ```csharp  
    button1.Location = new Point(100, 100);  
    ```  
  
    ```cpp  
    button1->Location = Point(100, 100);  
    ```  
  
2.  使用 <xref:System.Windows.Forms.Control.Left%2A> 子属性更改控件位置的 X 坐标。  
  
    ```vb  
    Button1.Left = 300  
    ```  
  
    ```csharp  
    button1.Left = 300;  
    ```  
  
    ```cpp  
    button1->Left = 300;  
    ```  
  
### 以编程方式增加控件的位置坐标  
  
1.  设置 <xref:System.Windows.Forms.Control.Left%2A> 子属性可增加控件的 X 坐标。  
  
    ```vb  
    Button1.Left += 200  
    ```  
  
    ```csharp  
    button1.Left += 200;  
    ```  
  
    ```cpp  
    button1->Left += 200;  
    ```  
  
    > [!NOTE]
    >  使用 <xref:System.Windows.Forms.Control.Location%2A> 属性可同时设置控件的 X 和 Y 位置。  若要分别设置位置的两个坐标，请使用控件的 <xref:System.Windows.Forms.Control.Left%2A>（**“X”**）或 <xref:System.Windows.Forms.Control.Top%2A>（**“Y”**）子属性。  由于表示按钮位置的 <xref:System.Drawing.Point> 结构包含该按钮坐标的“副本”，所以不要尝试隐式设置该结构的 X 坐标和 Y 坐标。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)   
 [How to: Set the Screen Location of Windows Forms](http://msdn.microsoft.com/zh-cn/cb023ab7-dea7-4284-9aa6-8c03c59b60c6)