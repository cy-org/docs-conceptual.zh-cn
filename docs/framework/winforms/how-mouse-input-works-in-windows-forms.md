---
title: "Windows 窗体中鼠标输入的工作原理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "鼠标, input"
  - "Windows 窗体, 鼠标输入"
ms.assetid: 48fc5240-75a6-44bf-9fce-6aa21b49705a
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Windows 窗体中鼠标输入的工作原理
接收和处理鼠标输入是每个 Windows 应用程序的重要组成部分。  您可以通过处理鼠标事件来执行应用程序中的操作，或者使用鼠标位置信息来执行命中测试或其他操作。  另外，还可以更改应用程序中控件处理鼠标输入的方式。  本主题详细描述这些鼠标事件，以及如何获取和更改鼠标的系统设置。  有关与鼠标事件一起提供的数据和鼠标单击事件的引发顺序的更多信息，请参见 [Windows 窗体中的鼠标事件](../../../docs/framework/winforms/mouse-events-in-windows-forms.md)。  
  
## 鼠标位置和命中测试  
 当用户移动鼠标时，操作系统会移动鼠标指针。  鼠标指针包含一个称为作用点的像素，操作系统跟踪作用点并将其识别为指针的位置。  当用户移动鼠标或按下鼠标按钮时，包含 <xref:System.Windows.Forms.Cursor.HotSpot%2A> 的 <xref:System.Windows.Forms.Control> 将引发相应的鼠标事件。  处理鼠标事件时，可以使用 <xref:System.Windows.Forms.MouseEventArgs> 的 <xref:System.Windows.Forms.MouseEventArgs.Location%2A> 属性来获取当前鼠标的位置，也可以使用 <xref:System.Windows.Forms.Cursor> 类的 <xref:System.Windows.Forms.Cursor.Position%2A> 属性来获取当前鼠标的位置。  其后可以使用鼠标位置信息来执行命中测试，再根据鼠标的位置执行操作。  命中测试功能内置于多个 Windows 窗体控件中，如 <xref:System.Windows.Forms.ListView>、<xref:System.Windows.Forms.TreeView>、<xref:System.Windows.Forms.MonthCalendar> 和 <xref:System.Windows.Forms.DataGridView> 控件。  当命中测试与适当的鼠标事件（例如 <xref:System.Windows.Forms.Control.MouseHover>）一起使用时，命中测试对于确定应用程序应在何时执行特定操作十分有用。  
  
## 鼠标事件  
 响应鼠标输入的主要方式是处理鼠标事件。  下表列出鼠标事件并描述其引发条件。  
  
|鼠标事件|说明|  
|----------|--------|  
|<xref:System.Windows.Forms.Control.Click>|释放鼠标按钮时发生此事件，通常发生在 <xref:System.Windows.Forms.Control.MouseUp> 事件前。  此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。  如果只需要确定何时发生单击，可处理此事件。|  
|<xref:System.Windows.Forms.Control.MouseClick>|用户使用鼠标单击控件时发生此事件。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。  如果需要在发生单击时获取鼠标的有关信息，可处理此事件。|  
|<xref:System.Windows.Forms.Control.DoubleClick>|双击控件时发生此事件。  此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。  如果只需要确定何时发生双击，可处理此事件。|  
|<xref:System.Windows.Forms.Control.MouseDoubleClick>|用户使用鼠标双击控件时发生此事件。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。  如果需要在发生双击时获取鼠标的有关信息，可处理此事件。|  
|<xref:System.Windows.Forms.Control.MouseDown>|当鼠标指针在控件上且用户按下鼠标按钮时发生此事件。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseEnter>|当鼠标指针进入控件的边框或工作区（具体取决于控件类型）时发生此事件。  此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseHover>|当鼠标指针停留在控件上时发生此事件。  此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseLeave>|当鼠标指针离开控件的边框或工作区（具体取决于控件类型）时发生此事件。  此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseMove>|当鼠标指针在控件上移动时发生此事件。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseUp>|当鼠标指针在控件上且用户释放鼠标按钮时发生此事件。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.MouseWheel>|如果用户在控件具有焦点时滚动鼠标轮，则发生此事件。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.MouseEventArgs> 的参数。  可以使用 <xref:System.Windows.Forms.MouseEventArgs> 的 <xref:System.Windows.Forms.MouseEventArgs.Delta%2A> 属性来确定鼠标滚动的距离。|  
  
## 更改鼠标输入并检测系统设置  
 您可以检测和更改控件处理鼠标输入的方式，方法是从该控件派生并使用 <xref:System.Windows.Forms.Control.GetStyle%2A> 和 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法。  <xref:System.Windows.Forms.Control.SetStyle%2A> 方法采用 <xref:System.Windows.Forms.ControlStyles> 值的按位组合来确定控件是具有标准的单击或双击行为，还是处理自己的鼠标行为。  另外，<xref:System.Windows.Forms.SystemInformation> 类包含一些属性，这些属性描述鼠标功能并指定鼠标与操作系统之间的互动方式。  下表总结了这些属性。  
  
|属性|说明|  
|--------|--------|  
|<xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A>|获取特定区域的尺寸（以像素为单位），用户必须在该区域内单击两次，操作系统才会将这两次单击视为一次双击。|  
|<xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A>|获取第一次单击和第二次单击之间可经过的最大毫秒数，只有两次单击的时间间隔不超过它，操作系统才会将该鼠标操作视为一次双击。|  
|<xref:System.Windows.Forms.SystemInformation.MouseButtons%2A>|获取鼠标上的按钮数。|  
|<xref:System.Windows.Forms.SystemInformation.MouseButtonsSwapped%2A>|获取一个值，该值指示是否已交换鼠标左右按钮的功能。|  
|<xref:System.Windows.Forms.SystemInformation.MouseHoverSize%2A>|获取特定矩形的尺寸（以像素为单位），鼠标指针必须在该矩形范围内停留达到鼠标悬停时间后，才会生成鼠标悬停消息。|  
|<xref:System.Windows.Forms.SystemInformation.MouseHoverTime%2A>|获取一个以毫秒为单位的时间，鼠标指针必须在悬停矩形中停留该时间后，才会生成鼠标悬停消息。|  
|<xref:System.Windows.Forms.SystemInformation.MousePresent%2A>|获取一个值，该值指示鼠标是否已安装。|  
|<xref:System.Windows.Forms.SystemInformation.MouseSpeed%2A>|获取一个指示当前鼠标速度的值，该值从 1 到 20。|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelPresent%2A>|获取一个值，该值指示是否安装了带有鼠标轮的鼠标。|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelScrollDelta%2A>|获取滚动一下鼠标轮的增量值。|  
|<xref:System.Windows.Forms.SystemInformation.MouseWheelScrollLines%2A>|获取滚动鼠标轮时所滚动过的行数。|  
  
## 请参阅  
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)   
 [Windows 窗体中的鼠标捕获](../../../docs/framework/winforms/mouse-capture-in-windows-forms.md)   
 [Windows 窗体中的鼠标指针](../../../docs/framework/winforms/mouse-pointers-in-windows-forms.md)