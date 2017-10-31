---
title: "如何：水平拆分窗口 | Microsoft Docs"
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
  - "SplitContainer 控件 [Windows 窗体], 水平拆分器"
  - "拆分窗口, 更改拆分器方向"
  - "拆分窗口, horizontal"
  - "窗口, 水平拆分"
ms.assetid: a1f74f29-048c-4723-85fa-b9d375ab8f4b
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：水平拆分窗口
下面的代码示例生成了一个水平拆分 <xref:System.Windows.Forms.SplitContainer> 控件的拆分器。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.SplitContainer> 控件的 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性确定拆分器的方向，而不是确定控件自身的方向。  
  
### 水平拆分窗口  
  
1.  在程序中，将 <xref:System.Windows.Forms.SplitContainer> 控件的 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性设置为 <xref:System.Windows.Forms.Orientation>。  
  
    ```vb  
    Sub ShowSplitContainer()  
        Dim splitContainer1 as new SplitContainer()  
        splitContainer1.BorderStyle = BorderStyle.Fixed3D  
        splitContainer1.Location = New System.Drawing.Point(74, 20)  
        splitContainer1.Name = "DemoSplitContainer"  
        splitContainer1.Size = New System.Drawing.Size(212, 435)  
        splitContainer1.TabIndex = 0  
        splitContainer1.Orientation = Orientation.Horizontal  
        Controls.Add(splitContainer1)  
    End Sub  
  
    ```  
  
    ```csharp  
    public void showSplitContainer()  
    {  
        SplitContainer splitContainer1 = new SplitContainer ();  
        splitContainer1.BorderStyle = BorderStyle.Fixed3D;  
        splitContainer1.Location = new System.Drawing.Point (74, 20);  
        splitContainer1.Name = "DemoSplitContainer";  
        splitContainer1.Size = new System.Drawing.Size (212, 435);  
        splitContainer1.TabIndex = 0;  
        splitContainer1.Orientation = Orientation.Horizontal;  
        this.Controls.Add (splitContainer1);  
  
    }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 [SplitContainer 控件](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)