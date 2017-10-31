---
title: "重写 OnPaint 方法 | Microsoft Docs"
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
  - "OnPaint 方法, 在 Windows 窗体自定义控件中重写"
  - "Paint 事件, 在 Windows 窗体自定义控件中处理"
ms.assetid: e9ca2723-0107-4540-bb21-4f5ffb4a9906
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 重写 OnPaint 方法
重写 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中定义的任何事件的基本步骤都是相同的，下表对其进行了总结。  
  
#### 重写继承事件  
  
1.  重写受保护的 `On`*事件名称* 方法。  
  
2.  从重写的 `On`*事件名称* 方法调用基类的 `On`*事件名称* 方法，以使注册的委托能够接收相应事件。  
  
 这里将详细介绍 <xref:System.Windows.Forms.Control.Paint> 事件，因为每个 Windows 窗体控件都必须重写从 <xref:System.Windows.Forms.Control> 继承的 <xref:System.Windows.Forms.Control.Paint> 事件。  <xref:System.Windows.Forms.Control> 基类不知道如何绘制派生控件，而且没有在 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法中提供任何绘制逻辑。  <xref:System.Windows.Forms.Control> 的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法只是将 <xref:System.Windows.Forms.Control.Paint> 事件调度到注册的事件接收器中。  
  
 如果看过 [如何：开发简单的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md) 中的示例，则应看过重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法的示例。  以下代码片段即摘自该示例。  
  
```vb  
Public Class FirstControl  
   Inherits Control  
  
   Public Sub New()  
   End Sub  
  
   Protected Overrides Sub OnPaint(e As PaintEventArgs)  
      ' Call the OnPaint method of the base class.  
      MyBase.OnPaint(e)  
      ' Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, New SolidBrush(ForeColor), RectangleF.op_Implicit(ClientRectangle))  
   End Sub  
End Class   
```  
  
```csharp  
public class FirstControl : Control{  
   public FirstControl() {}  
   protected override void OnPaint(PaintEventArgs e) {  
      // Call the OnPaint method of the base class.  
      base.OnPaint(e);  
      // Call methods of the System.Drawing.Graphics object.  
      e.Graphics.DrawString(Text, Font, new SolidBrush(ForeColor), ClientRectangle);  
   }   
}   
```  
  
 <xref:System.Windows.Forms.PaintEventArgs> 类包含 <xref:System.Windows.Forms.Control.Paint> 事件的数据。  它有两个属性，如以下代码所示。  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   ...  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property   
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs {  
...  
    public System.Drawing.Rectangle ClipRectangle {}  
    public System.Drawing.Graphics Graphics {}  
...  
}  
```  
  
 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 是要绘制的矩形，而 <xref:System.Windows.Forms.PaintEventArgs.Graphics%2A> 属性引用 <xref:System.Drawing.Graphics> 对象。  <xref:System.Drawing?displayProperty=fullName> 命名空间中的类是指提供对 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]（新 Windows 图形库）功能的访问的托管类。  <xref:System.Drawing.Graphics> 对象有绘制点、字符串、直线、圆弧、椭圆和许多其他形状的方法。  
  
 控件在需要改变其外观显示时将调用其 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  该方法随后引发 <xref:System.Windows.Forms.Control.Paint> 事件。  
  
## 请参阅  
 [事件](../../../../docs/standard/events/index.md)   
 [呈现 Windows 窗体控件](../../../../docs/framework/winforms/controls/rendering-a-windows-forms-control.md)   
 [定义事件](../../../../docs/framework/winforms/controls/defining-an-event-in-windows-forms-controls.md)