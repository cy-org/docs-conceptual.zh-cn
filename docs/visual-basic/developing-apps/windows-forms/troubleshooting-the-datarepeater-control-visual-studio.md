---
title: "DataRepeater 控件疑难解答 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 疑难解答"
ms.assetid: c0ab9469-eced-4f52-aa18-4bd8dd4f1a9a
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# DataRepeater 控件疑难解答 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

本主题列出了在使用 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件时可能会出现的一些常见问题。  
  
## 未能引发 DataRepeater 键盘和鼠标事件  
 未能引发某些 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件事件，如键盘和鼠标事件。  这是设计使然。  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件自身是 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 对象的容器，不能在运行时访问。  <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 在设计时不公开事件。  因此，当某个项具有焦点时单击该项或按键盘键不能引发事件。  
  
 这种情况的例外是：<xref:System.Windows.Forms.Control.Padding%2A> 属性设置为足够大的值，暴露了 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的边缘。  在这种情况下，在暴露的边距内单击会引发鼠标事件。  
  
 若要解决此问题，请向 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 部分添加一个 <xref:System.Windows.Forms.Panel> 控件，再将其他控件添加到 <xref:System.Windows.Forms.Panel> 中。  然后可以向 <xref:System.Windows.Forms.Panel> 控件的键盘和鼠标事件的事件处理程序中添加代码。  
  
## DataRepeater 部分隐藏在绑定导航器后面  
 当首次将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件添加到窗体中，然后从**“数据源”**窗口中添加数据绑定控件时，<xref:System.Windows.Forms.BindingNavigator> 控件可能会显示在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的顶部。  这是**“数据源”**窗口的一个已知局限性，与其他控件（如 <xref:System.Windows.Forms.DataGridView> 控件）的行为一致。  
  
 您可以在设计时移动 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>，使其低于 <xref:System.Windows.Forms.BindingNavigator> 控件，或向 `Load` 事件处理程序中添加与下面类似的代码。  
  
```vb#  
DataRepeater1.Top = ProductsBindingNavigator.Height  
```  
  
```c#  
dataRepeater1.Top = productsBindingNavigator.Height;  
```  
  
## 运行时某些控件无法正确显示  
 运行时 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中的某些控件不能按照预期的方式显示。  用于将控件从 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemTemplate%2A> 克隆到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 的过程并不能总是确定所有控件的所有属性。  例如，如果在设计时将未绑定的 <xref:System.Windows.Forms.ListBox> 控件添加到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件并用字符串列表填充它的 <xref:System.Windows.Forms.ListBox.Items%2A> 集合，则 <xref:System.Windows.Forms.ListBox> 在运行时将为空。  这是因为克隆过程无法考虑 <xref:System.Windows.Forms.ListBox.Items%2A> 属性。  
  
 您可以通过在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemCloned> 事件（该事件在默认克隆过程完成之后发生）中还原缺少的属性来解决此类问题。  下面的示例演示如何在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemCloned> 事件处理程序中修复 <xref:System.Windows.Forms.ListBox> 的 <xref:System.Windows.Forms.ListBox.Items%2A> 集合。  
  
 [!code-cs[VbPowerPacksDataRepeaterItemCloned#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/troubleshooting-the-datarepeater-control-visual-studio_1.cs)]
 [!code-vb[VbPowerPacksDataRepeaterItemCloned#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/troubleshooting-the-datarepeater-control-visual-studio_1.vb)]  
  
## 项标头上缺少选择符号  
 当您在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件中更改项标头的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 属性时，所选的某些颜色可能会导致选择符号消失。  更改 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> 属性也可能会导致选择符号消失。  
  
 不能更改选择符号的颜色和大小。  
  
-   如果将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 设置为 <xref:System.Drawing.Color.White%2A>，在首次选定某项时将看不到选择符号。  
  
-   如果将 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.SelectionColor%2A> 设置为 <xref:System.Drawing.Color.Black%2A>，当选定某个控件时将看不到选择符号，并且当控件处于编辑模式时看不到铅笔符号。  
  
-   如果 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.ItemHeaderSize%2A> 属性设置为小于 11 的值，项标头中将不会显示指示符。  
  
 您可以通过使用 <xref:System.Windows.Forms.PictureBox> 控件并在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件中监视 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 的 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A> 属性来提供自己的项标头和选择符号。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem.IsCurrent%2A>。  
  
## 请参阅  
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示未绑定的控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的布局](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-layout-of-a-datarepeater-control-visual-studio.md)   
 [如何：更改 DataRepeater 控件的外观](../../../visual-basic/developing-apps/windows-forms/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示项标题](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)   
 [如何：禁止添加和删除 DataRepeater 项](../../../visual-basic/developing-apps/windows-forms/how-to-disable-adding-and-deleting-datarepeater-items-visual-studio.md)   
 [如何：在 DataRepeater 控件中搜索数据](../../../visual-basic/developing-apps/windows-forms/how-to-search-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：使用两个 DataRepeater 控件创建主\/详细信息窗体](../../../visual-basic/developing-apps/windows-forms/how-to-create-a-master-detail-form-by-using-two-datarepeater-controls.md)