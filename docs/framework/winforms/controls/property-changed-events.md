---
title: "属性更改事件 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 属性更改（使用代码）"
  - "属性 [Windows 窗体], 更改"
ms.assetid: 268039ec-5aaa-4d76-b902-acccb036c850
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 属性更改事件
如果希望控件在名为*属性名称* 的属性发生更改时发送通知，则请定义一个名为*属性名称*`Changed` 的事件，以及一个名为 `On`*属性名称*`Changed` 的方法来引发该事件。  Windows 窗体中的命名规则是在属性的名称后追加 *Changed* 一词。  property\-changed 事件的关联事件委托类型为 <xref:System.EventHandler>，事件数据类型为 <xref:System.EventArgs>。  <xref:System.Windows.Forms.Control> 基类定义了许多 property\-changed 事件，例如 <xref:System.Windows.Forms.Control.BackColorChanged>、<xref:System.Windows.Forms.Control.BackgroundImageChanged>、<xref:System.Windows.Forms.Control.FontChanged>、<xref:System.Windows.Forms.Control.LocationChanged> 等。  有关事件的背景信息，请参见 [事件](../../../../docs/standard/events/index.md) 和 [Windows 窗体控件中的事件](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)。  
  
 Property\-changed 事件非常有用，因为它们允许控件的使用者附加对更改进行响应的事件处理程序。  如果控件需要对它所引发的 property\-changed 事件进行响应，则需要重写相应的 `On`*属性名称*`Changed` 方法，而不是给事件附加委托。  控件通常通过更新其他属性或重新绘制某些或全部绘制图面，对 property\-changed 事件作出响应。  
  
 下面的示例演示 `FlashTrackBar` 自定义控件对某些继承自 <xref:System.Windows.Forms.Control> 的 property\-changed 事件的响应方式。  有关完整示例，请参见 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#2)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#2)]  
  
## 请参阅  
 [事件](../../../../docs/standard/events/index.md)   
 [Windows 窗体控件中的事件](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)   
 [Windows 窗体控件中的属性](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)