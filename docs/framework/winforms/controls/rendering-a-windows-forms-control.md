---
title: "呈现 Windows 窗体控件 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 图形资源"
  - "自定义控件 [Windows 窗体], 无效和绘制"
  - "自定义控件 [Windows 窗体], 呈现"
  - "OnPaintBackground 方法, 在 Windows 窗体自定义控件中调用"
ms.assetid: aae8e1e6-4786-432b-a15e-f4c44760d302
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 呈现 Windows 窗体控件
呈现是指在用户屏幕上创建可视化表示的过程。  Windows 窗体使用 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)]（新的 Windows 图形库）来完成呈现。  提供对 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 进行访问的托管类位于 <xref:System.Drawing?displayProperty=fullName> 命名空间及其子命名空间中。  
  
 控件呈现中包括以下元素：  
  
-   由基类 <xref:System.Windows.Forms.Control?displayProperty=fullName> 提供的绘制功能。  
  
-   [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 图形库的基本元素。  
  
-   绘图区域的几何图形。  
  
-   释放图形资源的步骤。  
  
## 由控件提供的绘图功能  
 基类 <xref:System.Windows.Forms.Control> 通过其 <xref:System.Windows.Forms.Control.Paint> 事件提供绘制功能。  控件在需要更新其显示时引发 <xref:System.Windows.Forms.Control.Paint> 事件。  有关 .NET Framework 中事件的更多信息，请参见[处理和引发事件](../../../../docs/standard/events/index.md)。  
  
 <xref:System.Windows.Forms.Control.Paint> 事件的事件数据类 <xref:System.Windows.Forms.PaintEventArgs> 保存绘制控件所需的数据，即表示绘制区域的图形对象和矩形对象的句柄。  这些对象在以下代码段中显示为粗体。  
  
```vb  
Public Class PaintEventArgs  
   Inherits EventArgs  
   Implements IDisposable  
  
   Public ReadOnly Property ClipRectangle() As System.Drawing.Rectangle  
      ...  
   End Property  
  
   Public ReadOnly Property Graphics() As System.Drawing.Graphics  
      ...  
   End Property  
   ' Other properties and methods.  
   ...  
End Class  
```  
  
```csharp  
public class PaintEventArgs : EventArgs, IDisposable {  
public System.Drawing.Rectangle ClipRectangle {get;}  
public System.Drawing.Graphics Graphics {get;}  
// Other properties and methods.  
...  
}  
```  
  
 <xref:System.Drawing.Graphics> 是一个封装了绘制功能的托管类，该内容将在本主题中稍后对 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 的讨论中详细介绍。  <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 是 <xref:System.Drawing.Rectangle> 结构的一个实例，它定义绘制控件的可用区域。  控件开发者可以使用控件的 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 属性计算 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A>，详情将在本主题稍后的几何图形论述中进行说明。  
  
 控件必须通过重写它从 <xref:System.Windows.Forms.Control> 继承的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法来提供呈现逻辑。  <xref:System.Windows.Forms.Control.OnPaint%2A> 通过传递给它的 <xref:System.Windows.Forms.PaintEventArgs> 实例的 <xref:System.Drawing.Design.PaintValueEventArgs.Graphics%2A> 和 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 属性来访问图形对象以及要在其中进行绘制的矩形。  
  
```vb  
Protected Overridable Sub OnPaint(pe As PaintEventArgs)  
```  
  
```csharp  
protected virtual void OnPaint(PaintEventArgs pe);  
```  
  
 <xref:System.Windows.Forms.Control> 基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法不实现任何绘制功能，而仅仅是调用使用 <xref:System.Windows.Forms.Control.Paint> 事件注册的事件委托。  当重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 时，通常应调用基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，以便已注册的委派可以接收到 <xref:System.Windows.Forms.Control.Paint> 事件。  但是，绘制其整个图面的控件不应调用基类的 <xref:System.Windows.Forms.Control.OnPaint%2A>，因为这样会引起闪烁。  有关重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 事件的示例，请参见 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)。  
  
> [!NOTE]
>  不要直接从控件调用 <xref:System.Windows.Forms.Control.OnPaint%2A>，而应调用 <xref:System.Windows.Forms.Control.Invalidate%2A> 方法（继承自 <xref:System.Windows.Forms.Control>）或其他某个调用 <xref:System.Windows.Forms.Control.Invalidate%2A> 的方法。  <xref:System.Windows.Forms.Control.Invalidate%2A> 方法随后调用 <xref:System.Windows.Forms.Control.OnPaint%2A>。  <xref:System.Windows.Forms.Control.Invalidate%2A> 方法被重载，根据提供给 <xref:System.Windows.Forms.Control.Invalidate%2A> `e` 的参数，控件将重绘其部分或全部屏幕区域。  
  
 基类 <xref:System.Windows.Forms.Control> 定义了另一个可用于绘制的方法，即 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 方法。  
  
```vb  
Protected Overridable Sub OnPaintBackground(pevent As PaintEventArgs)  
```  
  
```csharp  
protected virtual void OnPaintBackground(PaintEventArgs pevent);  
```  
  
 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 绘制窗口的背景（即形状），并能保证快速完成，而 <xref:System.Windows.Forms.Control.OnPaint%2A> 绘制的是详细内容，并且由于各个绘制请求都组合到一个涵盖所有必须重绘的区域的 <xref:System.Windows.Forms.Control.Paint> 事件中，速度可能会慢一些。  在某些情况下（例如需要为控件绘制颜色渐变的背景），您可能需要调用 <xref:System.Windows.Forms.Control.OnPaintBackground%2A>。  
  
 虽然 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 的命名法与事件类似，并具有与 `OnPaint` 方法相同的参数，但 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 不是真正的事件方法。  没有 `PaintBackground` 事件，并且 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 不调用事件委托。  当重写 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 方法时，不要求派生类调用其基类的 <xref:System.Windows.Forms.Control.OnPaintBackground%2A> 方法。  
  
## GDI\+ 基础  
 <xref:System.Drawing.Graphics> 类提供了绘制各种形状（如圆、三角形、圆弧和椭圆）的方法，同时也提供了显示文本的方法。  <xref:System.Drawing?displayProperty=fullName> 命名空间及其子命名空间包含有封装了图形元素的类，图形元素包括形状（圆、矩形、圆弧及其他形状）、颜色、字体和笔刷等。  有关 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)]的更多信息，请参见[使用托管图形类](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md)。  [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 的要点在 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md) 中也有介绍。  
  
## 绘图区域的几何图形  
 控件的 <xref:System.Windows.Forms.Control.ClientRectangle%2A> 属性指定用户屏幕上控件可用的矩形区域，而 <xref:System.Windows.Forms.PaintEventArgs> 的 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 属性指定实际绘制的区域。  （切记，绘制是在 <xref:System.Windows.Forms.Control.Paint> 事件方法中完成的，该方法的参数中包含一个 <xref:System.Windows.Forms.PaintEventArgs> 实例）。  在控件的一小部分显示发生变化时，控件可能仅需要绘制其可用区域的一部分。  在这些情况下，控件开发者必须计算要在其中绘图的实际矩形并将其传递给 <xref:System.Windows.Forms.Control.Invalidate%2A>。  将 <xref:System.Drawing.Rectangle> 或 <xref:System.Drawing.Region> 作为一个参数的 <xref:System.Windows.Forms.Control.Invalidate%2A> 的重载版本使用该参数生成 <xref:System.Windows.Forms.PaintEventArgs> 的 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 属性。  
  
 以下代码段展示了 `FlashTrackBar` 自定义控件如何计算要在其中进行绘制的矩形区域。  `client` 变量表示 <xref:System.Windows.Forms.PaintEventArgs.ClipRectangle%2A> 属性。  有关完整示例，请参见 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#6)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#6)]  
  
## 释放图形资源  
 图形对象非常昂贵，因为它们占用很多系统资源。  此类对象包括 <xref:System.Drawing.Graphics?displayProperty=fullName> 类的实例以及 <xref:System.Drawing.Brush?displayProperty=fullName>、<xref:System.Drawing.Pen?displayProperty=fullName> 和其他图形类的实例。  应该仅在需要时才创建图形资源，并在使用完毕后立即将其释放，这一点非常重要。  如果创建一个实现 <xref:System.IDisposable> 界面的类型，请在使用完毕后调用其 <xref:System.IDisposable.Dispose%2A> 方法以释放资源。  
  
 下面的代码片段展示了 `FlashTrackBar` 自定义控件如何创建和释放 <xref:System.Drawing.Brush> 资源。  有关完整的源代码，请参见 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)。  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#5)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#5)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#4)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#4)]  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#3)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#3)]  
  
## 请参阅  
 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)