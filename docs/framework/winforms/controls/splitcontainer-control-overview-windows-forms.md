---
title: "SplitContainer 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "SplitContainer"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "SplitContainer 控件 [Windows 窗体], 关于 SplitContainer 控件"
ms.assetid: 6de5a5f7-97a5-402d-be6d-7e2785483db5
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# SplitContainer 控件概述（Windows 窗体）
可以将 Windows 窗体 <xref:System.Windows.Forms.SplitContainer> 控件看作是一个复合体，它是由一个可移动的拆分条分隔的两个面板。  当鼠标指针悬停在该拆分条上时，指针将相应地改灰度校正状以显示该拆分条是可移动的。  
  
> [!IMPORTANT]
>  在**“工具箱”**中，<xref:System.Windows.Forms.SplitContainer> 控件替换了早期版本的 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中存在的 <xref:System.Windows.Forms.Splitter> 控件。  <xref:System.Windows.Forms.SplitContainer> 控件在优先级上比 <xref:System.Windows.Forms.Splitter> 控件要高得多。  为了与现有的应用程序兼容，<xref:System.Windows.Forms.Splitter> 类仍包括在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中，但强烈建议您在新项目中使用 <xref:System.Windows.Forms.SplitContainer> 控件。  
  
 使用 <xref:System.Windows.Forms.SplitContainer> 控件，可以创建复合的用户界面（通常，在一个面板中的选择决定了在另一个面板中显示哪些对象）。  这种排列对于显示和浏览信息非常有用。  拥有两个面板使您可以聚合不同区域中的信息，并且用户可以轻松地使用拆分条（也称为“拆分器”）调整面板的大小。  
  
 另外，还可以嵌套多个 <xref:System.Windows.Forms.SplitContainer> 控件，并且第二个 <xref:System.Windows.Forms.SplitContainer> 控件可以水平放置，从而产生上面板和下面板。  
  
 请注意，<xref:System.Windows.Forms.SplitContainer> 控件默认情况下可通过键盘来访问。如果 <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性设置为 `false`，用户可以按箭头键来移动拆分器。  
  
 <xref:System.Windows.Forms.SplitContainer> 控件的 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性确定拆分器的方向，而不是确定控件自身的方向。  因此，当该属性设置为 <xref:System.Windows.Forms.Orientation> 时，拆分器将垂直放置，从而产生左面板和右面板。  
  
 此外，还应注意 <xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A> 属性的值是随 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性的值变化的。  有关更多信息，请参见 <xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A> 属性。  
  
 还可以限制 <xref:System.Windows.Forms.SplitContainer> 控件的大小和移动。  <xref:System.Windows.Forms.SplitContainer.FixedPanel%2A> 属性决定调整 <xref:System.Windows.Forms.SplitContainer> 控件大小后，哪个面板将保持原来的大小，<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性则决定是否可以通过键盘或鼠标来移动拆分器。  
  
> [!NOTE]
>  即使 <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性设置为 `true`，仍然可以通过编程的方式（如使用 <xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 属性）来移动拆分器。  
  
 最后，<xref:System.Windows.Forms.SplitContainer> 控件的每个面板都具有用于确定其各自大小的属性。  
  
## 常用属性、方法和事件  
  
|名称|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.SplitContainer.FixedPanel%2A> 属性|确定调整 <xref:System.Windows.Forms.SplitContainer> 控件大小后，哪个面板将保持原来的大小。|  
|<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性|确定是否可以使用键盘或鼠标来移动拆分器。|  
|<xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性|确定拆分器是垂直放置还是水平放置。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 属性|确定从左边缘或上边缘到可移动拆分条的距离（以像素为单位）。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性|确定用户可以移动拆分器的最短距离（以像素为单位）。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterWidth%2A> 属性|确定拆分器的厚度（以像素为单位）。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterMoving> 事件|拆分器移动时发生。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterMoved> 事件|拆分器移动后发生。|  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 [SplitContainer 控件](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)   
 [SplitContainer Control Sample](http://msdn.microsoft.com/zh-cn/9015fad0-7108-4d85-a83a-a72d038c4f65)