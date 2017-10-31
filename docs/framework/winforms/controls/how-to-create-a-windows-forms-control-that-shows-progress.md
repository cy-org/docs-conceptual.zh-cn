---
title: "如何：创建显示进度的 Windows 窗体控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 创建"
  - "控件 [Windows 窗体], 进度跟踪"
  - "FlashTrackBar 自定义控件"
  - "进度, 报告 [Windows 窗体]"
ms.assetid: 24c5a2e3-058c-4b8d-a217-c06e6a130c2f
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：创建显示进度的 Windows 窗体控件
下面的代码示例演示一个名为 `FlashTrackBar` 的自定义控件，该控件可用于向用户显示应用程序的级别或进度。  它使用渐变以直观的方式表示进度。  
  
 `FlashTrackBar` 控件阐释了以下概念：  
  
-   定义自定义属性。  
  
-   定义自定义事件。  （`FlashTrackBar` 定义 `ValueChanged` 事件。）  
  
-   重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法以提供绘制控件的逻辑。  
  
-   通过使用其 <xref:System.Windows.Forms.Control.ClientRectangle%2A> 属性计算可用于绘制控件的区域。  `FlashTrackBar` 在其 `OptimizedInvalidate` 方法中执行此计算。  
  
-   当在 Windows 窗体设计器中更改属性时实现属性的序列化或持久性。  `FlashTrackBar` 定义 `ShouldSerializeStartColor` 和 `ShouldSerializeEndColor` 方法，以序列化其 `StartColor` 和 `EndColor` 属性。  
  
 下表显示由 `FlashTrackBar` 定义的自定义属性。  
  
|属性|说明|  
|--------|--------|  
|`AllowUserEdit`|指示用户是否可以通过单击和拖动来更改闪烁跟踪条的值。|  
|`EndColor`|指定跟踪条的结束颜色。|  
|`DarkenBy`|指定根据前景渐变加深背景颜色的程度。|  
|`Max`|指定跟踪条的最大值。|  
|`Min`|指定跟踪条的最小值。|  
|`StartColor`|指定渐变的开始颜色。|  
|`ShowPercentage`|指示是否在渐变之上显示百分比。|  
|`ShowValue`|指示是否在渐变之上显示当前值。|  
|`ShowGradient`|指示跟踪条是否应显示表明当前值的颜色渐变。|  
|-   `Value`|指定跟踪条的当前值。|  
  
 下表显示由 `FlashTrackBar:` 定义的附加成员：property\-changed 事件以及引发该事件的方法。  
  
|成员|说明|  
|--------|--------|  
|`ValueChanged`|当跟踪条的 `Value` 属性改变时引发的事件。|  
|`OnValueChanged`|引发 `ValueChanged` 事件的方法。|  
  
> [!NOTE]
>  `FlashTrackBar` 将 <xref:System.EventArgs> 类用于事件数据，将 <xref:System.EventHandler> 用于事件委托。  
  
 为了处理相应的*事件名称* 事件，`FlashTrackBar` 重写它从 <xref:System.Windows.Forms.Control?displayProperty=fullName> 继承的以下方法：  
  
-   <xref:System.Windows.Forms.Control.OnPaint%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseDown%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseMove%2A>  
  
-   <xref:System.Windows.Forms.Control.OnMouseUp%2A>  
  
-   <xref:System.Windows.Forms.Control.OnResize%2A>  
  
 为了处理相应的 property\-changed 事件，`FlashTrackBar` 重写它从 <xref:System.Windows.Forms.Control?displayProperty=fullName> 继承的以下方法：  
  
-   <xref:System.Windows.Forms.Control.OnBackColorChanged%2A>  
  
-   <xref:System.Windows.Forms.Control.OnBackgroundImageChanged%2A>  
  
-   <xref:System.Windows.Forms.Control.OnTextChanged%2A>  
  
## 示例  
 `FlashTrackBar` 控件定义两种用户界面类型编辑器：`FlashTrackBarValueEditor` 和 `FlashTrackBarDarkenByEditor`，如下面的代码清单所示。  `HostApp` 类在 Windows 窗体上使用 `FlashTrackBar` 控件。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#1)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#1)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarDarkenByEditor.cs#10)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarDarkenByEditor.vb#10)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBarValueEditor.cs#20)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBarValueEditor.vb#20)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/HostApp.cs#30)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/HostApp.vb#30)]  
  
## 请参阅  
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [Windows 窗体控件开发基础知识](../../../../docs/framework/winforms/controls/windows-forms-control-development-basics.md)