---
title: "如何：定义拆分窗口中的大小调整和定位行为 | Microsoft Docs"
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
  - "拆分窗口, 调整大小"
  - "SplitContainer 控件 [Windows 窗体], 调整大小"
  - "拆分窗口, 调整大小"
ms.assetid: 9bf73f36-ed2d-4a02-b15a-0770eff4fdfa
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：定义拆分窗口中的大小调整和定位行为
用户可以轻松调整 <xref:System.Windows.Forms.SplitContainer> 控件面板的大小并对其执行各种操作。  但是，有时您可能要以编程方式控制拆分器放置的位置以及可以移动的程度。  
  
 利用 <xref:System.Windows.Forms.SplitContainer> 控件上的 <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性和其他属性，您可以根据自己的需要精确控制用户界面的行为。  下表列出了这些属性。  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性|确定拆分器是否可以通过键盘或鼠标进行移动。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 属性|确定从左边缘或上边缘到可移动拆分条的距离（以像素为单位）。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性|确定用户可以移动拆分器的最短距离（以像素为单位）。|  
  
 下面的示例修改了 <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性，以创建“对齐拆分器”效果；在用户拖动拆分器时，它会以 10 个像素（而非默认的 1 个像素）为单位进行递增。  
  
### 定义 SplitContainer 调整大小行为  
  
1.  在过程中，将 <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性设置为所需大小，以实现拆分器的“对齐”行为。  
  
     在下面的代码示例中，在窗体的 <xref:System.Windows.Forms.Form.Load> 事件中将 <xref:System.Windows.Forms.SplitContainer> 控件中的拆分器设置为拖动时跳过 10 个像素。  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, _  
        ByVal e As System.EventArgs) Handles MyBase.Load  
        Dim splitSnapper as new SplitContainer()  
        splitSnapper.SplitterIncrement = 10  
        splitSnapper.Dock = DockStyle.Fill  
        splitSnapper.Parent = me  
    End Sub  
  
    ```  
  
    ```csharp  
    private void Form1_Load(System.Object sender, System.EventArgs e)  
    {  
        SplitContainer splitSnapper = new SplitContainer();  
        splitSnapper.SplitterIncrement = 10;  
        splitSnapper.Dock = DockStyle.Fill;  
        splitSnapper.Parent = this;  
    }  
    ```  
  
     \([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]\) 在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
     略微左移或右移拆分器不会产生明显的效果；但是，当鼠标指针向左、右任一方向移动 10 个像素时，拆分器将对齐新的位置。  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 <xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A>