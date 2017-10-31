---
title: "如何：在 FlowLayoutPanel 控件中锚定和停靠子控件 | Microsoft Docs"
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
  - "子控件, 锚定和停靠"
  - "控件 [Windows 窗体], 子控件"
  - "FlowLayoutPanel 控件 [Windows 窗体], 子控件"
  - "布局 [Windows 窗体], 子控件"
ms.assetid: a2bcdfca-9b63-45e6-9c0e-3411015cba98
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在 FlowLayoutPanel 控件中锚定和停靠子控件
<xref:System.Windows.Forms.FlowLayoutPanel> 控件支持其子控件中的 <xref:System.Windows.Forms.Control.Anchor%2A> 和 <xref:System.Windows.Forms.Control.Dock%2A> 属性。  
  
### 在 FlowLayoutPanel 控件中锚定和停靠子控件  
  
1.  在窗体上创建一个 <xref:System.Windows.Forms.FlowLayoutPanel> 控件。  
  
2.  将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.Control.Width%2A> 设置为 300，并将其 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 设置为 <xref:System.Windows.Forms.FlowDirection>。  
  
3.  创建两个 <xref:System.Windows.Forms.Button> 控件，并将它们放入 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中。  
  
4.  将第一个按钮的 <xref:System.Windows.Forms.Control.Width%2A> 设置为 200。  
  
5.  将第二个按钮的 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
    > [!NOTE]
    >  第二个按钮采用与第一个按钮相同的宽度。  它不在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的宽度范围内拉伸。  
  
6.  将第二个按钮的 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为`无`。  这将导致该按钮采用其原始的宽度。  
  
7.  将第二个按钮的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性设置为 `Left, Right（左、右）`。  
  
    > [!IMPORTANT]
    >  第二个按钮采用与第一个按钮相同的宽度。  它不在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的宽度范围内拉伸。  这是在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中锚定和停靠的一般规则：对于垂直流方向，<xref:System.Windows.Forms.FlowLayoutPanel> 控件计算列中最宽子控件的隐含列的宽度。  对齐或拉伸此列中具有 <xref:System.Windows.Forms.Control.Anchor%2A> 或 <xref:System.Windows.Forms.Control.Dock%2A> 属性的所有其他控件以适合此隐含列。  该行为以相似的方式在水平流方向工作。  <xref:System.Windows.Forms.FlowLayoutPanel> 控件计算行中最高子控件的隐含行的高度，并对齐此行中所有停靠的或锚定的子控件或调整其大小以适应隐含行。  
  
## 示例  
 下图显示了四个按钮，它们相对于 <xref:System.Windows.Forms.FlowLayoutPanel> 中的蓝色按钮锚定和停靠。  <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 为 <xref:System.Windows.Forms.FlowDirection>。  
  
 ![FlowLayoutPanel 锚定](../../../../docs/framework/winforms/controls/media/net-flpanchorexp.png "NET\_FLPanchorExp")  
  
 下图显示了四个按钮，它们相对于 <xref:System.Windows.Forms.FlowLayoutPanel> 中的蓝色按钮锚定和停靠。  <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 为 <xref:System.Windows.Forms.FlowDirection>。  
  
 ![FlowLayoutPanel 锚定](../../../../docs/framework/winforms/controls/media/vs-flpanchor2.png "VS\_FLPanchor2")  
  
 以下代码示例演示了 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中 <xref:System.Windows.Forms.Button> 控件的各种 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值。  
  
 [!code-csharp[System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm/CS/FlpAnchorExampleForm.cs#1)]
 [!code-vb[System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlowLayoutPanel.AnchorExampleForm/VB/FlpAnchorExampleForm.vb#1)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Data、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 <xref:System.Windows.Forms.FlowLayoutPanel>   
 [FlowLayoutPanel 控件概述](../../../../docs/framework/winforms/controls/flowlayoutpanel-control-overview.md)