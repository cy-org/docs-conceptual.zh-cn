---
title: "如何：在 DataRepeater 控件中显示项标题 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 项标头"
  - "DataRepeater, 选择指示器"
ms.assetid: 37321447-0ffa-43e1-bdc9-0480e392b90f
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 如何：在 DataRepeater 控件中显示项标题 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

<xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中的项标头会在选定了某个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 时提供直观的指示。  当 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> 属性设置为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles>（默认值）时，项标头会显示在每个项的左侧。  当 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> 属性设置为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles> 时，项标头会显示在每个项的顶部。  
  
 首次选定项标头时，它将以 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 属性指定的颜色显示，并且还将显示一个白色箭头图标。  
  
> [!NOTE]
>  如果 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 设置为 <xref:System.Drawing.Color.White%2A>，当首次选定项时您将看不到选择符号。  
  
 当 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 中的某个字段具有焦点时，项标头的颜色将变为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 背景颜色并且箭头图标将变为黑色。  如果数据发生更改，项标头中会显示一个铅笔符号。  
  
 项标头的默认宽度（如果 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.LayoutStyle%2A> 属性设置为 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterLayoutStyles>，则为高度）为 15 像素。  可以通过设置 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> 属性来更改此宽度。  
  
> [!NOTE]
>  如果 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> 属性设置为小于 11 的值，项标头中将不会显示指示符。  
  
 可以通过将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderVisible%2A> 属性设置为**“False”**来隐藏项标头。  当 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderVisible%2A> 设置为**“False”**时，表示选定了某个项的唯一指示是该 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 周围的虚线。  
  
> [!NOTE]
>  您还可以通过在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件中监视 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A> 属性来提供自己的选择指示符。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A>。  
  
### 更改项标头的外观  
  
1.  在 Windows 窗体设计器中，选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的下半部分区域。  
  
    > [!NOTE]
    >  必须选择控件的下半部分区域。  如果选择项模板部分，“属性”窗口中将显示一组不同的属性。  
  
2.  在“属性”窗口中使用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 属性来更改项标头的颜色。  
  
    > [!NOTE]
    >  如果 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 设置为 <xref:System.Drawing.Color.White%2A>，当首次选定项时您将看不到选择符号。  
  
3.  使用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> 属性来更改项标头的宽度（或高度）。  
  
    > [!NOTE]
    >  如果 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> 属性设置为小于 11 的值，项标头中将不会显示指示符。  
  
### 隐藏项标头  
  
1.  在 Windows 窗体设计器中，选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的下半部分区域。  
  
    > [!NOTE]
    >  必须选择控件的下半部分区域。  如果选择项模板部分，“属性”窗口中将显示一组不同的属性。  
  
2.  在“属性”窗口中，将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderVisible%2A> 属性设置为**“False”**。  
  
     当选定了 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 中的某个项时，唯一的指示将是该 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 周围的虚线。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的布局](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)