---
title: "创建墨迹输入控件 | Microsoft Docs"
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
  - "收集墨迹笔画"
  - "DynamicRenderer 对象"
  - "墨迹输入控件"
  - "墨迹笔画, 收集"
  - "墨迹笔画, 管理"
  - "墨迹, Rendering — 呈现"
  - "从鼠标输入, 接受"
  - "管理墨迹笔画"
  - "鼠标输入, 接受"
  - "呈现墨迹"
  - "StylusPlugIn 对象"
ms.assetid: c31f3a67-cb3f-4ded-af9e-ed21f6575b26
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 创建墨迹输入控件
您可以创建一个既能动态呈现墨迹又能静态呈现墨迹的自定义控件。  更确切地说，动态呈现是指用户边画笔画边呈现墨迹（这样，墨迹看上去好像是从触笔中“画出”的），静态呈现是指在通过触笔、从剪贴板中粘贴或从文件中加载的方式将墨迹添加到控件之后显示墨迹。  若要动态呈现墨迹，您的控件必须使用 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>。  若要静态呈现墨迹，必须重写触笔事件方法（<xref:System.Windows.UIElement.OnStylusDown%2A>、<xref:System.Windows.UIElement.OnStylusMove%2A> 和 <xref:System.Windows.UIElement.OnStylusUp%2A>）以收集 <xref:System.Windows.Input.StylusPoint> 数据、创建笔画以及将笔画添加到 <xref:System.Windows.Controls.InkPresenter>（在控件上呈现墨迹）。  
  
 本主题包含以下小节：  
  
-   [如何：收集触笔接触点数据和创建墨迹笔画](#CollectingStylusPointDataAndCreatingInkStrokes)  
  
-   [如何：使控件能够接受通过鼠标输入的内容](#EnablingYourControlToAcceptInputTromTheMouse)  
  
-   [将内容结合起来](#PuttingItTogether)  
  
-   [使用附加的插件和 DynamicRenderers](#UsingAdditionalPluginsAndDynamicRenderers)  
  
-   [结束语](#AdvancedInkHandling_Conclusion)  
  
<a name="CollectingStylusPointDataAndCreatingInkStrokes"></a>   
## 如何：收集触笔接触点数据和创建墨迹笔画  
 若要创建收集和管理墨迹笔画的控件，请执行下列操作：  
  
1.  从 <xref:System.Windows.Controls.Control> 或派生自 <xref:System.Windows.Controls.Control> 的一个类中派生一个类，例如 <xref:System.Windows.Controls.Label>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
    [!code-csharp[AdvancedInkTopicsSamples#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#14)]  
    [!code-csharp[AdvancedInkTopicsSamples#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#15)]  
  
2.  将 <xref:System.Windows.Controls.InkPresenter> 添加至类并将 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性设置为新的 <xref:System.Windows.Controls.InkPresenter>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#16)]  
  
3.  通过调用 <xref:System.Windows.Controls.InkPresenter.AttachVisuals%2A> 方法将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> 附加至 <xref:System.Windows.Controls.InkPresenter>，并将 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 添加至 <xref:System.Windows.UIElement.StylusPlugIns%2A> 集合。  这样，在控件收集触笔接触点数据时，<xref:System.Windows.Controls.InkPresenter> 可以显示墨迹。  
  
     [!code-csharp[AdvancedInkTopicsSamples#17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#17)]  
    [!code-csharp[AdvancedInkTopicsSamples#18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#18)]  
  
4.  重写 <xref:System.Windows.UIElement.OnStylusDown%2A> 方法。  在此方法中，通过对 <xref:System.Windows.Input.Stylus.Capture%2A> 的调用来获取触笔。  通过获取触笔，控件将继续接收 <xref:System.Windows.UIElement.StylusMove> 和 <xref:System.Windows.UIElement.StylusUp> 事件，即使触笔离开了控件的边界也是如此。  虽然并不一定要执行此操作，但是为了获得良好的用户体验，几乎总是需要进行此操作。  创建新的 <xref:System.Windows.Input.StylusPointCollection> 以收集 <xref:System.Windows.Input.StylusPoint> 数据。  最后，将最初的 <xref:System.Windows.Input.StylusPoint> 数据集添加至 <xref:System.Windows.Input.StylusPointCollection>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#7)]  
  
5.  重写 <xref:System.Windows.UIElement.OnStylusMove%2A> 方法并将 <xref:System.Windows.Input.StylusPoint> 数据添加至以前创建的 <xref:System.Windows.Input.StylusPointCollection> 对象。  
  
     [!code-csharp[AdvancedInkTopicsSamples#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#8)]  
  
6.  重写 <xref:System.Windows.UIElement.OnStylusUp%2A> 方法并用 <xref:System.Windows.Input.StylusPointCollection> 数据创建新的 <xref:System.Windows.Ink.Stroke>。  将所创建的新 <xref:System.Windows.Ink.Stroke> 添加至 <xref:System.Windows.Controls.InkPresenter> 的 <xref:System.Windows.Controls.InkPresenter.Strokes%2A> 集合中并释放触笔捕获。  
  
     [!code-csharp[AdvancedInkTopicsSamples#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#10)]  
  
<a name="EnablingYourControlToAcceptInputTromTheMouse"></a>   
## 如何：使控件能够接受通过鼠标输入的内容  
 如果向应用程序添加了上述控件，运行此应用程序，并使用鼠标作为输入设备，则您将会发现笔画不持久。  若要在将鼠标用作输入设备时使笔画持久化，请执行下列操作：  
  
1.  重写 <xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A> 并创建新的 <xref:System.Windows.Input.StylusPointCollection>。获取鼠标在发生事件时的位置，使用接触点数据创建 <xref:System.Windows.Input.StylusPoint>，并将 <xref:System.Windows.Input.StylusPoint> 添加至 <xref:System.Windows.Input.StylusPointCollection>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#11)]  
  
2.  重写 <xref:System.Windows.UIElement.OnMouseMove%2A> 方法。  获取鼠标在发生事件时的位置，并使用接触点数据创建 <xref:System.Windows.Input.StylusPoint>。  将 <xref:System.Windows.Input.StylusPoint> 添加至以前创建的 <xref:System.Windows.Input.StylusPointCollection> 对象。  
  
     [!code-csharp[AdvancedInkTopicsSamples#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#12)]  
  
3.  重写 <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> 方法。  用 <xref:System.Windows.Input.StylusPointCollection> 数据创建新的 <xref:System.Windows.Ink.Stroke>，并将所创建的新 <xref:System.Windows.Ink.Stroke> 添加至 <xref:System.Windows.Controls.InkPresenter> 的 <xref:System.Windows.Controls.InkPresenter.Strokes%2A> 集合。  
  
     [!code-csharp[AdvancedInkTopicsSamples#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#13)]  
  
<a name="PuttingItTogether"></a>   
## 将内容结合起来  
 下面的示例是一个自定义控件，它在用户使用鼠标或笔时收集墨迹。  
  
 [!code-csharp[AdvancedInkTopicsSamples#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
[!code-csharp[AdvancedInkTopicsSamples#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#6)]  
  
<a name="UsingAdditionalPluginsAndDynamicRenderers"></a>   
## 使用附加的插件和 DynamicRenderers  
 与 InkCanvas 相似，自定义控件可以具有自定义的 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 和附加的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 对象。  将这些内容添加至 <xref:System.Windows.UIElement.StylusPlugIns%2A> 集合。  <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 中 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 对象的顺序会影响墨迹呈现时的外观。  假设您具有一个名为 `dynamicRenderer` 的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 以及一个名为 `translatePlugin` 的自定义 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>（会使触笔的墨迹发生偏移）。  如果 `translatePlugin` 是 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 中的第一个 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>，`dynamicRenderer` 是第二个，则当用户移动笔时所“画出”的墨迹将会偏移。  如果 `dynamicRenderer` 是第一个，`translatePlugin` 是第二个，则在用户提起笔之前，墨迹将不会偏移。  
  
<a name="AdvancedInkHandling_Conclusion"></a>   
## 结束语  
 通过重写触笔事件方法，您可以创建一个能够收集和呈现墨迹的控件。  通过创建自己的控件，派生自己的 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 类并将这些类插入到 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>，您几乎可以实现可想像的任何数字墨迹行为。  您可以在生成 <xref:System.Windows.Input.StylusPoint> 数据时访问该数据，从而有机会自定义 <xref:System.Windows.Input.Stylus> 输入并且适当时会在屏幕上为您的应用程序呈现它。  因为能够对 <xref:System.Windows.Input.StylusPoint> 数据进行这种低级别访问，所以可以在确保应用程序最佳性能的情况下实现墨迹收集和呈现墨迹。  
  
## 请参阅  
 [高级墨迹处理](../../../../docs/framework/wpf/advanced/advanced-ink-handling.md)   
 [Accessing and Manipulating Pen Input](http://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)