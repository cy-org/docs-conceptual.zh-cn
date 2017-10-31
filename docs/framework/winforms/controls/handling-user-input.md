---
title: "处理用户输入 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 使用代码的键盘事件"
  - "自定义控件 [Windows 窗体], 使用代码的鼠标事件"
  - "自定义控件 [Windows 窗体], 使用代码的用户输入"
ms.assetid: d9b12787-86f6-4022-8e0f-e12d312c4af2
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 处理用户输入
本主题描述了由 <xref:System.Windows.Forms.Control?displayProperty=fullName> 提供的主键盘和鼠标事件。  处理事件时，控件作者应该重写受保护的 `On`*事件名称* 方法，而不是向事件附加委托。  若要查看事件，请参见 [从组件引发事件](../Topic/Raising%20Events%20from%20a%20Component.md)。  
  
> [!NOTE]
>  如果没有与事件关联的数据，则会将基类 <xref:System.EventArgs> 的一个实例作为参数传递给 `On`*事件名称* 方法。  
  
## 键盘事件  
 您的控件可以处理的常见键盘事件包括 <xref:System.Windows.Forms.Control.KeyDown>、<xref:System.Windows.Forms.Control.KeyPress> 和 <xref:System.Windows.Forms.Control.KeyUp>。  
  
|事件名称|要重写的方法|事件说明|  
|----------|------------|----------|  
|`KeyDown`|`void OnKeyDown(KeyEventArgs)`|仅在开始按下键时引发。|  
|`KeyPress`|`void OnKeyPress`<br /><br /> `(KeyPressEventArgs)`|每次按键时引发。  如果一直按住某个键，则按操作系统定义的重复速率引发 <xref:System.Windows.Forms.Control.KeyPress> 事件。|  
|`KeyUp`|`void OnKeyUp(KeyEventArgs)`|释放键时引发。|  
  
> [!NOTE]
>  处理键盘输入比重写上表中的事件要复杂得多，这超出了本主题的讨论范围。  有关更多信息，请参见 [Windows 窗体中的用户输入](../../../../docs/framework/winforms/user-input-in-windows-forms.md)。  
  
## 鼠标事件  
 您的控件可以处理的鼠标事件包括 <xref:System.Windows.Forms.Control.MouseDown>、<xref:System.Windows.Forms.Control.MouseEnter>、<xref:System.Windows.Forms.Control.MouseHover>、<xref:System.Windows.Forms.Control.MouseLeave>、<xref:System.Windows.Forms.Control.MouseMove> 和 <xref:System.Windows.Forms.Control.MouseUp>。  
  
|事件名称|要重写的方法|事件说明|  
|----------|------------|----------|  
|`MouseDown`|`void OnMouseDown(MouseEventArgs)`|指针位于控件上时，按下鼠标按钮会引发该事件。|  
|`MouseEnter`|`void OnMouseEnter(EventArgs)`|当指针首次进入控件区域时引发。|  
|`MouseHover`|`void OnMouseHover(EventArgs)`|当指针悬停于控件上时引发。|  
|`MouseLeave`|`void OnMouseLeave(EventArgs)`|当指针离开控件区域时引发。|  
|`MouseMove`|`void OnMouseMove(MouseEventArgs)`|当指针在控件区域中移动时引发。|  
|`MouseUp`|`void OnMouseUp(MouseEventArgs)`|指针位于控件上或指针离开控件区域时，松开鼠标按钮会引发该事件。|  
  
 下面的代码片段演示了重写 <xref:System.Windows.Forms.Control.MouseDown> 事件的例子。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#7)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#7)]  
  
 下面的代码片段演示了重写 <xref:System.Windows.Forms.Control.MouseMove> 事件的例子。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#8](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#8)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#8](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#8)]  
  
 下面的代码片段演示了重写 <xref:System.Windows.Forms.Control.MouseUp> 事件的例子。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#9)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#9)]  
  
 有关 `FlashTrackBar` 示例的完整源代码，请参见 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)。  
  
## 请参阅  
 [Windows 窗体控件中的事件](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)   
 [定义事件](../../../../docs/framework/winforms/controls/defining-an-event-in-windows-forms-controls.md)   
 [事件](../../../../docs/standard/events/index.md)   
 [Windows 窗体中的用户输入](../../../../docs/framework/winforms/user-input-in-windows-forms.md)