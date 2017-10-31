---
title: "用户描述的控件 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 用户描述的"
  - "OnPaint 方法 [Windows 窗体]"
  - "用户绘制的控件 [Windows 窗体]"
ms.assetid: 034af4b5-457f-4160-a937-22891817faa8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 用户描述的控件
.NET Framework 使您得以轻松地开发自己的控件。  您可以用代码将一组标准控件绑定在一起来创建用户控件，也可以从头开始设计自己的控件。  甚至还可以利用继承性创建一个从现有控件继承的控件，并扩展该控件的固有功能。  无论采用哪种方法，.NET Framework 都提供为所创建的任何控件绘制自定义图形界面的功能。  
  
 控件的绘制是通过执行控件的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法中的代码实现的。  <xref:System.Windows.Forms.Control.OnPaint%2A> 方法的唯一参数是 <xref:System.Windows.Forms.PaintEventArgs> 对象，该对象提供了呈现控件所需的所有信息和功能。  <xref:System.Windows.Forms.PaintEventArgs> 提供作为属性的、用于呈现控件的两个主要对象：  
  
-   <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 对象 \-\- 表示要绘制的控件部分的一个矩形。  根据如何绘制控件，这可以是整个控件，也可以是部分控件。  
  
-   <xref:System.Drawing.Graphics> 对象 \-\- 该对象封装了几个面向图形的对象和方法，这些对象和方法提供绘制控件所需的功能。  
  
 有关 <xref:System.Drawing.Graphics> 对象及其使用方式的更多信息，请参见[如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)。  
  
 每当在屏幕上绘制或刷新控件时都会激发 <xref:System.Windows.Forms.Control.OnPaint%2A> 事件，<xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 对象表示将在其中进行绘制的矩形。  如果需要刷新整个控件，则 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 表示整个控件的大小。  然而，如果仅需要刷新控件的一部分，则 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 对象仅表示需要重新绘制的区域。  这类情况的一个示例是：某个控件被用户界面中的另一个控件或窗体部分遮挡时。  
  
 当从 <xref:System.Windows.Forms.Control> 类继承时，必须重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法并在其中提供呈现图形的代码。  如果要为用户控件或继承控件提供自定义图形界面，也可以通过重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法来完成此操作。  下面显示了一个示例：  
  
```vb  
Protected Overrides Sub OnPaint(ByVal pe As PaintEventArgs)  
   ' Call the OnPaint method of the base class.  
   MyBase.OnPaint(pe)  
  
   ' Declare and instantiate a drawing pen.  
   Dim myPen As System.Drawing.Pen = New System.Drawing.Pen(Color.Aqua)  
  
   ' Draw an aqua rectangle in the rectangle represented by the control.  
   pe.Graphics.DrawRectangle(myPen, New Rectangle(Me.Location, Me.Size))  
End Sub  
  
```  
  
```csharp  
protected override void OnPaint(PaintEventArgs pe)  
{  
   // Call the OnPaint method of the base class.  
   base.OnPaint(pe);  
  
   // Declare and instantiate a new pen.  
   System.Drawing.Pen myPen = new System.Drawing.Pen(Color.Aqua);  
  
   // Draw an aqua rectangle in the rectangle represented by the control.  
   pe.Graphics.DrawRectangle(myPen, new Rectangle(this.Location,   
      this.Size));  
}  
  
```  
  
 前面的示例示范了如何用非常简单的图形化表示形式呈现控件。  它调用基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，创建用来进行绘制的 <xref:System.Drawing.Pen> 对象，最后在由控件的 <xref:System.Windows.Forms.Control.Location%2A> 和 <xref:System.Windows.Forms.Control.Size%2A> 确定的矩形中绘制一个椭圆。  虽然大多数呈现代码都要比此示例复杂得多，但此示例演示了如何使用包含在 <xref:System.Windows.Forms.PaintEventArgs> 对象内的 <xref:System.Drawing.Graphics> 对象。  请注意，如果要从已有图形化表示形式的类（如 <xref:System.Windows.Forms.UserControl> 或 <xref:System.Windows.Forms.Button>）继承，而且不希望将该表示形式并入呈现中，则不应该调用基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
 在首次绘制控件和每次刷新控件时，都将执行控件的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法中的代码。  为了确保在每次调整控件大小时都重绘控件，请将下列代码行添加到控件的构造函数中：  
  
```vb  
SetStyle(ControlStyles.ResizeRedraw, True)  
  
```  
  
```csharp  
SetStyle(ControlStyles.ResizeRedraw, true);  
  
```  
  
> [!NOTE]
>  使用 <xref:System.Windows.Forms.Control.Region%2A?displayProperty=fullName> 属性来实现非矩形控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.Region%2A>   
 <xref:System.Windows.Forms.ControlStyles>   
 <xref:System.Drawing.Graphics>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 <xref:System.Windows.Forms.PaintEventArgs>   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [构成控件](../../../../docs/framework/winforms/controls/constituent-controls.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)