---
title: "事件处理程序概述（Windows 窗体） | Microsoft Docs"
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
  - "事件处理程序, 关于事件处理程序"
  - "事件处理, Windows 窗体"
  - "Windows 窗体, 事件处理"
ms.assetid: 228112e1-1711-42ee-8ffa-ff3555bffe66
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 事件处理程序概述（Windows 窗体）
事件处理程序是绑定到事件的方法。  当引发事件时，执行事件处理程序内的代码。  每个事件处理程序提供两个使您得以正确处理事件的参数。  下面的示例演示 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件的事件处理程序。  
  
```vb  
Private Sub button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles button1.Click  
  
End Sub  
  
```  
  
```csharp  
private void button1_Click(object sender, System.EventArgs e)   
{  
  
}  
  
```  
  
```cpp  
private:  
  void button1_Click(System::Object ^ sender,  
    System::EventArgs ^ e)  
  {  
  
  }  
```  
  
 第一个参数，`sender`，提供对引发事件的对象。  上面示例中的第二个参数 `e` 传递特定于要处理的事件的对象。  通过引用对象的属性（有时引用其方法）可获得一些信息，如鼠标事件中鼠标的位置或拖放事件中传输的数据。  
  
 通常每个事件都会为第二个参数产生一个具有不同事件对象类型的事件处理程序。  一些事件处理程序，如 <xref:System.Windows.Forms.Control.MouseDown> 和 <xref:System.Windows.Forms.Control.MouseUp> 事件的事件处理程序，对于其第二个参数具有相同的对象类型。  对于这些类型的事件，可使用相同的事件处理程序处理这两个事件。  
  
 也可使用相同的事件处理程序处理不同控件的同一事件。  例如，若在窗体上有一组 <xref:System.Windows.Forms.RadioButton> 控件，可创建单个 <xref:System.Windows.Forms.Control.Click> 事件的事件处理程序，并将每个控件的 <xref:System.Windows.Forms.Control.Click> 事件都绑定到该事件处理程序上。  有关更多信息，请参见 [如何：将多个事件连接到 Windows 窗体中的单个事件处理程序](../../../docs/framework/winforms/how-to-connect-multiple-events-to-a-single-event-handler-in-windows-forms.md)。  
  
## 请参阅  
 [在 Windows 窗体中创建事件处理程序](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [事件概述](../../../docs/framework/winforms/events-overview-windows-forms.md)