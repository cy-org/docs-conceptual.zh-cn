---
title: "如何：更改 DataRepeater 控件的布局 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 更改布局样式"
  - "DataRepeater, 更改方向"
ms.assetid: 33aa8fd5-ac63-4bd0-ba13-8c2ab17e7824
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 如何：更改 DataRepeater 控件的布局 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

可以沿垂直（项目垂直滚动）方向或水平（项目水平滚动）方向显示 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  您可以通过在设计时或运行时更改 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> 属性来更改方向。  如果在运行时更改 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> 属性，您可能还需要重新调整 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 的大小和重新定位子控件。  
  
> [!NOTE]
>  如果在运行时在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 上重新定位控件，您需要在用于重新定位控件的代码块的开头和结尾处调用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A> 和 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A> 方法。  
  
### 在设计时更改布局  
  
1.  在 Windows 窗体设计器中，选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件。  
  
    > [!NOTE]
    >  必须选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的外部边框，方法是单击该控件的下半部分区域，而不是单击上半部分的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 区域。  
  
2.  在“属性”窗口中，将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> 属性设置为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles> 或 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles>。  
  
### 在运行时更改布局  
  
1.  在按钮或菜单的 `Click` 事件处理程序中添加下面的代码：  
  
     [!code-cs[VbPowerPacksDataRepeaterLayout#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksDataRepeaterLayout#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_1.vb)]  
  
2.  在大多数情况下，您会希望添加类似于“示例”部分所示的代码来重新调整 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 的大小并重新排列控件，以适应新的方向。  
  
## 示例  
 下面的示例演示如何在事件处理程序中响应 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyleChanged> 事件。  此示例要求您在窗体上有一个名为 `DataRepeater1` 的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件，并且该控件的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 包含两个名称分别为 `TextBox1` 和 `TextBox2` 的 <xref:System.Windows.Forms.TextBox> 控件。  
  
 [!code-cs[VbPowerPacksDataRepeaterLayout#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_2.cs)]
 [!code-vb[VbPowerPacksDataRepeaterLayout#2](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-layout-of-a-datarepeater-control-visual-studio_2.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.BeginResetItemTemplate%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.EndResetItemTemplate%2A>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)