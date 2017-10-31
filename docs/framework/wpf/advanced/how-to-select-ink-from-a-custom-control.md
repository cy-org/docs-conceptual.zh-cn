---
title: "如何：从自定义控件选择墨迹 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件, 墨迹选择"
  - "自定义控件, 墨迹选择"
  - "墨迹, 从自定义控件选择"
ms.assetid: 5f3a45c6-6d40-4017-9b47-933f134ceba3
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：从自定义控件选择墨迹
通过向自定义控件中添加 <xref:System.Windows.Ink.IncrementalLassoHitTester>，您可以使控件具备如下功能：用户能使用套索工具选择墨迹，其方式与 <xref:System.Windows.Controls.InkCanvas> 使用套索选择墨迹的方式类似。  
  
 此示例假定您熟悉如何创建支持墨迹的自定义控件。  若要创建接受墨迹输入的自定义控件，请参见[创建墨迹输入控件](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md)。  
  
## 示例  
 当用户绘制套索时，<xref:System.Windows.Ink.IncrementalLassoHitTester> 会预测在用户完成套索之后哪些笔画将位于套索路径的边界内。  确定位于套索路径边界内的笔画可视为已选中。  选中的笔画也可变成未选中。  例如，如果用户在绘制套索时反转方向，则 <xref:System.Windows.Ink.IncrementalLassoHitTester> 可能会取消选择某些笔画。  
  
 <xref:System.Windows.Ink.IncrementalLassoHitTester> 引发 <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> 事件，该事件使自定义控件能在用户绘制套索时做出响应。  例如，您可以在用户选择和取消选择笔画时更改笔画的外观。  
  
## 管理墨迹模式  
 如果套索在控件上的显示方式与墨迹不一样，这对用户很有帮助。  若要实现这一点，自定义控件必须跟踪用户是在编写还是在选择墨迹。  最简单的方法是声明一个具有两个值的枚举：一个值指示用户正在编写墨迹，另一个值指示用户正在选择墨迹。  
  
 [!code-csharp[HowToSelectInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#2)]
 [!code-vb[HowToSelectInk#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#2)]  
  
 然后，向该类添加两个 <xref:System.Windows.Ink.DrawingAttributes>：一个用于用户编写墨迹时，另一个用于用户选择墨迹时。  在构造函数中，初始化 <xref:System.Windows.Ink.DrawingAttributes> 并将两个 <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> 事件附加到同一个事件处理程序。  再将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> 属性设置为墨迹 <xref:System.Windows.Ink.DrawingAttributes>。  
  
 [!code-csharp[HowToSelectInk#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#3)]
 [!code-vb[HowToSelectInk#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#3)]  
[!code-csharp[HowToSelectInk#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#4)]
[!code-vb[HowToSelectInk#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#4)]  
  
 添加一个公开选择模式的属性。  当用户更改选择模式时，将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> 属性设置为相应的 <xref:System.Windows.Ink.DrawingAttributes> 对象，然后重新将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> 属性附加到 <xref:System.Windows.Controls.InkPresenter>。  
  
 [!code-csharp[HowToSelectInk#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#5)]
 [!code-vb[HowToSelectInk#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#5)]  
  
 将 <xref:System.Windows.Ink.DrawingAttributes> 作为属性公开，以使应用程序可以决定墨迹笔画和选择笔画的外观。  
  
 [!code-csharp[HowToSelectInk#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#6)]
 [!code-vb[HowToSelectInk#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#6)]  
  
 当 <xref:System.Windows.Ink.DrawingAttributes> 对象的属性更改时，必须将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> 重新附加到 <xref:System.Windows.Controls.InkPresenter>。  在 <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> 事件的事件处理程序中，将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> 重新附加到 <xref:System.Windows.Controls.InkPresenter>。  
  
 [!code-csharp[HowToSelectInk#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#7)]
 [!code-vb[HowToSelectInk#7](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#7)]  
  
## 使用 IncrementalLassoHitTester  
 创建并初始化包含所选笔画的 <xref:System.Windows.Ink.StrokeCollection>。  
  
 [!code-csharp[HowToSelectInk#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#8)]
 [!code-vb[HowToSelectInk#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#8)]  
  
 当用户开始绘制笔画时，不管是墨迹还是套索，请取消选择任何已选中的笔画。  然后，如果用户要绘制套索，请通过调用 <xref:System.Windows.Ink.StrokeCollection.GetIncrementalLassoHitTester%2A> 创建一个 <xref:System.Windows.Ink.IncrementalLassoHitTester>，订阅 <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> 事件，然后再调用 <xref:System.Windows.Ink.IncrementalHitTester.AddPoints%2A>。  此代码可以是单独的方法，并且可以从 <xref:System.Windows.UIElement.OnStylusDown%2A> 和 <xref:System.Windows.UIElement.OnMouseDown%2A> 方法调用。  
  
 [!code-csharp[HowToSelectInk#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#9)]
 [!code-vb[HowToSelectInk#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#9)]  
  
 在用户绘制套索时，向 <xref:System.Windows.Ink.IncrementalLassoHitTester> 添加触笔接触点。  从 <xref:System.Windows.UIElement.OnStylusMove%2A>、<xref:System.Windows.UIElement.OnStylusUp%2A>、<xref:System.Windows.UIElement.OnMouseMove%2A> 和 <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> 方法调用以下方法。  
  
 [!code-csharp[HowToSelectInk#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#10)]
 [!code-vb[HowToSelectInk#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#10)]  
  
 处理 <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged?displayProperty=fullName> 事件，以便在用户选择和取消选择笔画时做出响应。  <xref:System.Windows.Ink.LassoSelectionChangedEventArgs> 类具有 <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.SelectedStrokes%2A> 和 <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.DeselectedStrokes%2A> 属性，用于分别获取已选中和取消选中的笔画。  
  
 [!code-csharp[HowToSelectInk#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#11)]
 [!code-vb[HowToSelectInk#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#11)]  
  
 当用户绘制完套索后，取消订阅 <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> 事件，然后调用 <xref:System.Windows.Ink.IncrementalHitTester.EndHitTesting%2A>。  
  
 [!code-csharp[HowToSelectInk#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#12)]
 [!code-vb[HowToSelectInk#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#12)]  
  
## 汇总所有内容。  
 下面的示例是一个自定义控件，用户可以通过该控件使用套索来选择墨迹。  
  
 [!code-csharp[HowToSelectInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#1)]
 [!code-vb[HowToSelectInk#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Ink.IncrementalLassoHitTester>   
 <xref:System.Windows.Ink.StrokeCollection>   
 <xref:System.Windows.Input.StylusPointCollection>   
 [创建墨迹输入控件](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md)