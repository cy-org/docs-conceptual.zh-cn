---
title: "拖放概述 | Microsoft Docs"
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
  - "数据传输 [WPF], 拖放"
  - "拖动源 [WPF], 拖放"
  - "拖放 [WPF], 关于"
  - "拖放 [WPF], 事件"
  - "拖放 [WPF], 实现"
  - "放置目标 [WPF], 拖放"
ms.assetid: 1a5b27b0-0ac5-4cdf-86c0-86ac0271fa64
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# 拖放概述
本主题概述 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中的拖放支持。  拖放通常指一种数据传输方法：使用鼠标（或一些其他指针设备）选择一个或多个对象，将其拖至 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中的某些所需拖放目标之上并放置。  
  
   
  
<a name="Drag_and_Drop_Support"></a>   
## WPF 中的拖放支持  
 拖放操作通常涉及两个参与方：拖动对象所源自的拖动源和接收放置对象的拖放目标。  拖动源和放置目标可能是相同应用程序或不同应用程序中的 UI 元素。  
  
 可借助拖放操纵的对象的类型和数量是完全任意的。  例如，文件、文件夹和内容选择是利用拖放操作操纵的一些常见对象。  
  
 拖放操作期间执行的特定操作特定于应用程序，并且通常由上下文而定。  例如，将选择的文件从一个文件夹一拖动至相同存储设备上的另一个文件夹将默认移动文件；而将文件从 [!INCLUDE[TLA#tla_unc](../../../../includes/tlasharptla-unc-md.md)] 共享拖动至本地文件夹将默认复制文件。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的拖放设施拥有高度的灵活性并可自定义，以便支持各种拖放方案。  拖放支持在单个应用程序内或不同应用程序之间操作对象。  也完全支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序和其它 [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)] 应用程序之间的拖放。  
  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，任何 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 都可以参与拖放。  拖放操作所需的事件和方法是在 <xref:System.Windows.DragDrop> 类中定义的。  <xref:System.Windows.UIElement> 和 <xref:System.Windows.ContentElement> 类包含 <xref:System.Windows.DragDrop> 附加事件的别名，从而在 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 作为基元素继承时，这些事件出现在类成员列表中。  附加到这些事件的事件处理程序会附加到基础 <xref:System.Windows.DragDrop> 附加事件，并接收相同的事件数据实例。  有关详细信息，请参阅 <xref:System.Windows.UIElement.Drop?displayProperty=fullName> 事件。  
  
> [!IMPORTANT]
>  在 Internet 区域中 OLE 拖放无效。  
  
<a name="Data_Transfer"></a>   
## 数据传输  
 拖放属于广义的数据传输。  数据传输包括拖放和复制粘贴操作。  拖放操作类似于用于借助系统剪贴板将数据从一个对象或应用程序传输到另一个对象或应用程序的复制粘贴或剪切和粘贴操作。  这两种类型的操作均要求：  
  
-   提供数据的源对象。  
  
-   用于临时存储传输的数据的方法。  
  
-   接收数据的目标对象。  
  
 在复制粘贴操作中，系统剪贴板用于临时存储传输的数据；在拖放操作中，<xref:System.Windows.DataObject> 用于存储数据。  从概念上讲，数据对象由一对或多对包含实际数据的 <xref:System.Object> 和对应的数据格式标识符组成。  
  
 拖动源通过调用静态 <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=fullName> 方法和向其传递传输的数据来启动拖放操作。  如有必要，<xref:System.Windows.DragDrop.DoDragDrop%2A> 方法将使 <xref:System.Windows.DataObject> 中的数据自动换行。  为了更好地控制数据格式，可将 <xref:System.Windows.DataObject> 中的数据换行，然后再将其传递至 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法。  拖放目标负责从 <xref:System.Windows.DataObject> 中提取数据。  有关使用数据对象的详细信息，请参阅[数据和数据对象](../../../../docs/framework/wpf/advanced/data-and-data-objects.md)。  
  
 拖放操作的源和目标均为 UI 元素；然而，实际正在传输的数据通常不具有可视表示形式。  可以编写代码来提供拖动的数据的可视表示形式（比如当在 Windows 资源管理器中拖动文件时会出现这种情况）。  默认情况下，通过更改光标将反馈提供给用户，以便表示拖放操作将对数据产生的影响，例如将移动数据还是复制数据。  
  
### 拖放效果  
 拖放操作对传输的数据可具有不同的效果。  例如，可以复制数据，或者可以移动数据。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义可用于指定拖放操作效果的 <xref:System.Windows.DragDropEffects> 枚举。  在拖动源中，可以指定源在 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法中允许的效果。  在拖放目标中，可以指定目标在 <xref:System.Windows.DragEventArgs> 类的 <xref:System.Windows.DragEventArgs.Effects%2A> 属性的中预期的效果。  当拖放目标指定其在 <xref:System.Windows.DragDrop.DragOver> 事件中的预期效果时，该信息将被传递回 <xref:System.Windows.DragDrop.GiveFeedback> 事件中的拖动源。  拖动源则使用此信息通知用户拖放目标想要对数据产生的效果。  放置数据时，拖放目标指定其在 <xref:System.Windows.DragDrop.Drop> 事件中的实际效果。  该信息会作为 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法的返回值传递回拖动源。  如果拖放目标返回并不在 `allowedEffects` 拖动源列表中的效果，那么将取消拖放操作，且不会进行任何数据传输。  
  
 请务必记住，在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，<xref:System.Windows.DragDropEffects> 值仅用于提供有关拖放操作效果的拖动源和拖放目标之间的通信。  拖放操作的实际效果取决于你在应用程序中编写的相应代码。  
  
 例如，拖放目标可以指定在其中放置数据的效果是移动数据。  然而，若要移动数据，必须将数据添加到目标元素并从源元素中删除数据。  源元素可能指示允许移动数据，但是如果没有提供从源元素中删除数据的代码，那么最终结果将为复制但不删除数据。  
  
<a name="Drag_and_Drop_Events"></a>   
## 拖放事件  
 拖放操作支持事件驱动模型。  拖动源和拖放目标都使用一组标准的事件来处理拖放操作。  下表总结了标准的拖放事件。  它们是 <xref:System.Windows.DragDrop> 类中的附加事件。  有关附加事件的详细信息，请参阅[附加事件概述](../../../../docs/framework/wpf/advanced/attached-events-overview.md)。  
  
### 拖动源事件  
  
|Event|摘要|  
|-----------|--------|  
|<xref:System.Windows.DragDrop.GiveFeedback>|此事件在拖放操作期间持续发生，并且使放置源能够向用户提供反馈信息。  通常通过更改鼠标指针外观来指示拖放目标允许的效果这一方式来提供这种反馈。  这是 [冒泡](GTMT)事件。|  
|<xref:System.Windows.DragDrop.QueryContinueDrag>|此事件于拖放操作期间键盘或鼠标按钮状态发生变化时发生，并使放置源能够根据键\/按钮状态取消拖放操作。  这是冒泡事件。|  
|<xref:System.Windows.DragDrop.PreviewGiveFeedback>|<xref:System.Windows.DragDrop.GiveFeedback> 的 [隧道](GTMT)版本。|  
|<xref:System.Windows.DragDrop.PreviewQueryContinueDrag>|<xref:System.Windows.DragDrop.QueryContinueDrag> 的隧道版本。|  
  
### 拖放目标事件  
  
|Event|摘要|  
|-----------|--------|  
|<xref:System.Windows.DragDrop.DragEnter>|将对象拖到拖放目标的边界中时发生此事件。  这是冒泡事件。|  
|<xref:System.Windows.DragDrop.DragLeave>|将对象拖出拖放目标边界时发生此事件。  这是冒泡事件。|  
|<xref:System.Windows.DragDrop.DragOver>|在拖放目标的边界内拖动（移动）对象时会持续发生此事件。  这是冒泡事件。|  
|<xref:System.Windows.DragDrop.Drop>|将对象放置在拖放目标上时发生此事件。  这是冒泡事件。|  
|<xref:System.Windows.DragDrop.PreviewDragEnter>|<xref:System.Windows.DragDrop.DragEnter> 的隧道版本。|  
|<xref:System.Windows.DragDrop.PreviewDragLeave>|<xref:System.Windows.DragDrop.DragLeave> 的隧道版本。|  
|<xref:System.Windows.DragDrop.PreviewDragOver>|<xref:System.Windows.DragDrop.DragOver> 的隧道版本。|  
|<xref:System.Windows.DragDrop.PreviewDrop>|<xref:System.Windows.DragDrop.Drop> 的隧道版本。|  
  
 若要处理对象实例的拖放事件，请为上表中所列的事件添加处理程序。  若要处理类级别的拖放事件，请重写相应的虚拟 On\* Event 和 On\* PreviewEvent 方法。  有关详细信息，请参阅[按控件基类进行路由事件的类处理](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md#Class_Handling_of_Routed_Events)。  
  
<a name="Implementing_Drag_And_Drop"></a>   
## 实现拖放  
 UI 元素可以是拖动源、拖放目标或两者均可。  若要实现基本拖放，请编写用于启动拖放操作和处理放置的数据的代码。  可以通过处理可选拖放事件增强拖放体验。  
  
 若要实现基本拖放，将完成以下任务：  
  
-   标识将作为拖动源的元素。  拖动源可以是 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement>。  
  
-   在将启动拖放操作的拖动源上创建事件处理程序。  此事件通常是 <xref:System.Windows.UIElement.MouseMove> 事件。  
  
-   在拖动源事件处理程序中，调用 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法启动拖放操作。  在 <xref:System.Windows.DragDrop.DoDragDrop%2A> 调用中，指定拖动源、要传输的数据和允许的效果。  
  
-   标识将作为拖放目标的元素。  拖放目标可以是 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement>。  
  
-   在拖放目标上，将 <xref:System.Windows.UIElement.AllowDrop%2A> 属性设置为 `true`。  
  
-   在拖放目标中，创建 <xref:System.Windows.DragDrop.Drop> 事件处理程序以处理放置的数据。  
  
-   在 <xref:System.Windows.DragDrop.Drop> 事件处理程序中，利用 <xref:System.Windows.DataObject.GetDataPresent%2A> 和 <xref:System.Windows.DataObject.GetData%2A> 方法提取 <xref:System.Windows.DragEventArgs> 中的数据。  
  
-   在 <xref:System.Windows.DragDrop.Drop> 事件处理程序中，使用数据来执行所需的拖放操作。  
  
 可以通过创建自定义 <xref:System.Windows.DataObject> 和处理可选拖动源和拖放目标事件来增加拖放实现，如以下任务中所示：  
  
-   若要传输自定义数据或多个数据项，请创建一个 <xref:System.Windows.DataObject>以传递至 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法。  
  
-   若要在拖动过程中执行其他操作，请处理拖放目标上的 <xref:System.Windows.DragDrop.DragEnter><xref:System.Windows.DragDrop.DragOver> 和 <xref:System.Windows.DragDrop.DragLeave> 事件。  
  
-   若要更改鼠标指针外观，请处理拖动源上的 <xref:System.Windows.DragDrop.GiveFeedback> 事件。  
  
-   若要更改取消拖放操作的方式，请处理拖动源上的 <xref:System.Windows.DragDrop.QueryContinueDrag> 事件。  
  
<a name="Drag_And_Drop_Example"></a>   
## 拖放示例  
 本节介绍如何实现 <xref:System.Windows.Shapes.Ellipse> 元素的拖放。  <xref:System.Windows.Shapes.Ellipse> 既是拖动源也是拖放目标。  传输的数据是椭圆形的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性的字符串表示形式。  下面的 XAML 展示 <xref:System.Windows.Shapes.Ellipse> 元素和它处理的拖放相关事件。  有关如何实现拖放的完整步骤，请参阅[演练：对用户控件启用拖放功能](../../../../docs/framework/wpf/advanced/walkthrough-enabling-drag-and-drop-on-a-user-control.md)。  
  
 [!code-xml[DragDropSnippets#EllipseXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#ellipsexaml)]  
  
### 使元素作为拖动源  
 拖动源对象用于：  
  
-   标识拖动发生的时候。  
  
-   启动拖放操作。  
  
-   标识要传输的数据。  
  
-   指定允许拖放操作对传输的数据产生的效果。  
  
 拖动源还可能针对允许的操作（移动、复制、无）向用户提供反馈，并且可以根据额外用户输入（如拖动过程中按 ESC 键）取消拖放操作。  
  
 你的应用程序负责确定发生拖动的时间，然后通过调用 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法启动拖放操作。  通常情况下，这是在按下鼠标按钮的同时，要拖动的元素上发生 <xref:System.Windows.UIElement.MouseMove> 事件时。  下面的示例显示了如何从 <xref:System.Windows.Shapes.Ellipse> 元素的 <xref:System.Windows.UIElement.MouseMove> 事件处理程序中启动拖放操作，以将其作为拖动源。  传输的数据是椭圆形的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性的字符串表示形式。  
  
 [!code-csharp[DragDropSnippets#DoDragDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dodragdrop)]
 [!code-vb[DragDropSnippets#DoDragDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dodragdrop)]  
  
 在 <xref:System.Windows.UIElement.MouseMove> 事件处理程序中，调用 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法启动拖放操作。  <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法采用三个参数：  
  
-   `dragSource` – 引用作为传输的数据的源的依赖项对象；通常是 <xref:System.Windows.UIElement.MouseMove> 事件的源。  
  
-   `data` \- 包含传输的数据（包装在 <xref:System.Windows.DataObject> 中）的对象。  
  
-   `allowedEffects` \- 指定拖放操作允许的效果的 <xref:System.Windows.DragDropEffects> 枚举值之一。  
  
 任何可序列化对象都可以在 `data` 参数中传递。  如果数据尚未包装在 <xref:System.Windows.DataObject> 中，则它将自动包装在一个新的 <xref:System.Windows.DataObject> 中。  若要传递多个数据项，必须自行创建 <xref:System.Windows.DataObject>，并将其传递到 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法。  有关详细信息，请参阅[数据和数据对象](../../../../docs/framework/wpf/advanced/data-and-data-objects.md)。  
  
 `allowedEffects` 参数用于指定拖动源允许拖放目标对传输的数据进行什么操作。  拖动源公共值为 <xref:System.Windows.DragDropEffects><xref:System.Windows.DragDropEffects> 和<xref:System.Windows.DragDropEffects>。  
  
> [!NOTE]
>  拖放目标也能够指定其对放置的数据的预期效果。  例如，如果拖放目标不能识别要放置的数据类型，则可以通过将其允许的效果设置为 <xref:System.Windows.DragDropEffects> 来拒绝数据。  通常在其 <xref:System.Windows.DragDrop.DragOver> 事件处理程序中进行此操作。  
  
 拖动源还可以可选地处理 <xref:System.Windows.DragDrop.GiveFeedback> 和 <xref:System.Windows.DragDrop.QueryContinueDrag> 事件。  这些事件都具有使用的默认处理程序，除非将事件标记为已处理。  通常将忽略这些事件，除非有更改其默认行为的特定需要。  
  
 对拖动源进行拖动时，持续引发 <xref:System.Windows.DragDrop.GiveFeedback> 事件。  此事件的默认处理程序会检查拖动源是否在有效拖放目标之上。  如果是，它会检查拖放目标的允许的效果。  然后向最终用户提供有关允许的放置效果的反馈。  通常通过将鼠标光标更改为非放置、复制或移动光标实现此操作。  仅在需要使用自定义光标向用户提供反馈时处理此事件。  在处理此事件时，请务必将其标记为“已处理”，以便默认处理程序不会替代你的处理程序。  
  
 对拖动源进行拖动时，持续引发 <xref:System.Windows.DragDrop.QueryContinueDrag> 事件。  你可以根据 ESC、SHIFT、CTRL 和 ALT 键以及鼠标按钮的状态处理此事件，以确定结束拖放操作的操作。  此事件的默认处理程序在按下 ESC 键后取消拖放操作，并且在释放鼠标按钮后放置数据。  
  
> [!CAUTION]
>  在拖放操作过程中，将持续引发这些事件。  因此，应避免事件处理程序中的资源密集型任务。  例如，每次引发 <xref:System.Windows.DragDrop.GiveFeedback> 事件时，请使用缓存的光标，而不是创建新光标。  
  
### 使元素作为拖放目标  
 作为拖放目标的对象用于：  
  
-   指定其是有效的拖放目标。  
  
-   当它拖动到目标之上时，向拖动源作出响应。  
  
-   检查传输的数据是否是它可以接收的格式。  
  
-   处理已放置的数据。  
  
 若要指定一个元素是拖放目标，请将其 <xref:System.Windows.UIElement.AllowDrop%2A> 属性设置为 `true`。  然后，元素中将引发拖放目标事件，以便处理这些事件。  在拖放操作期间，拖放目标上将依次发生以下事件：  
  
1.  <xref:System.Windows.DragDrop.DragEnter>  
  
2.  <xref:System.Windows.DragDrop.DragOver>  
  
3.  <xref:System.Windows.DragDrop.DragLeave> 或 <xref:System.Windows.DragDrop.Drop>  
  
 将数据拖到拖放目标的边界中时发生 <xref:System.Windows.DragDrop.DragEnter> 事件。  通常，如果适用于你的应用程序，可处理此事件，以便提供拖放操作效果预览。  请勿设置 <xref:System.Windows.DragDrop.DragEnter> 事件中的 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> 属性，因为在 <xref:System.Windows.DragDrop.DragOver> 事件中该属性将被覆盖。  
  
 下面的示例演示 <xref:System.Windows.Shapes.Ellipse> 元素的 <xref:System.Windows.DragDrop.DragEnter> 事件处理程序。  此代码通过保存当前的 <xref:System.Windows.Shapes.Shape.Fill%2A> 画笔预览拖放操作的效果。  然后，它使用 <xref:System.Windows.DataObject.GetDataPresent%2A> 方法来检查是否已将 <xref:System.Windows.DataObject> 拖动到包含可以转换为 <xref:System.Windows.Media.Brush> 的字符串数据的椭圆上方。  如果是，则使用 <xref:System.Windows.DataObject.GetData%2A> 方法提取数据。  然后将其转换为 <xref:System.Windows.Media.Brush> 并应用于椭圆。  在 <xref:System.Windows.DragDrop.DragLeave> 事件处理程序中还原更改。  如果数据无法转换为 <xref:System.Windows.Media.Brush>，则不执行任何操作。  
  
 [!code-csharp[DragDropSnippets#DragEnter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragenter)]
 [!code-vb[DragDropSnippets#DragEnter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragenter)]  
  
 将数据拖动到拖放目标上方时持续发生 <xref:System.Windows.DragDrop.DragOver> 事件。  此事件和拖动源上的 <xref:System.Windows.DragDrop.GiveFeedback> 事件成对出现。  在 <xref:System.Windows.DragDrop.DragOver> 事件处理程序中，通常使用 <xref:System.Windows.DataObject.GetDataPresent%2A> 和 <xref:System.Windows.DataObject.GetData%2A> 方法来检查传输的数据是否是拖放目标可以处理的格式。  还可以检查是否已按下修改键，这通常指示用户想进行移动操作还是复制操作。  执行这些检查后，设置 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> 属性以通知拖动源放置数据将产生的效果。  拖动源收到 <xref:System.Windows.DragDrop.GiveFeedback> 事件参数中的此信息，并且可以设置相应的光标以向用户提供反馈。  
  
 下面的示例演示 <xref:System.Windows.Shapes.Ellipse> 元素的 <xref:System.Windows.DragDrop.DragOver> 事件处理程序。  此代码检查是否已将 <xref:System.Windows.DataObject> 拖动到包含可以转换为 <xref:System.Windows.Media.Brush> 的字符串数据的椭圆上方。  如果是，它会将 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.DragDropEffects>。  这将向拖动源指示可以将数据复制到椭圆。  如果数据无法转换为 <xref:System.Windows.Media.Brush>，则将 <xref:System.Windows.DragEventArgs.Effects%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.DragDropEffects>。  这将向拖动源指示椭圆不是数据的有效拖放目标。  
  
 [!code-csharp[DragDropSnippets#DragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragover)]
 [!code-vb[DragDropSnippets#DragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragover)]  
  
 将数据拖出目标边界而未放置时，发生 <xref:System.Windows.DragDrop.DragLeave> 事件。  可以处理此事件，以便撤销在 <xref:System.Windows.DragDrop.DragEnter> 事件处理程序中进行的一切操作。  
  
 下面的示例演示 <xref:System.Windows.Shapes.Ellipse> 元素的 <xref:System.Windows.DragDrop.DragLeave> 事件处理程序。  此代码通过将保存的 <xref:System.Windows.Media.Brush> 应用到椭圆来撤销 <xref:System.Windows.DragDrop.DragEnter> 事件处理程序中执行的预览。  
  
 [!code-csharp[DragDropSnippets#DragLeave](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#dragleave)]
 [!code-vb[DragDropSnippets#DragLeave](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#dragleave)]  
  
 数据放置在拖放目标上方时，发生 <xref:System.Windows.DragDrop.Drop> 事件；默认情况下，释放鼠标按钮时，发生此事件。  在 <xref:System.Windows.DragDrop.Drop> 事件处理程序中，使用 <xref:System.Windows.DataObject.GetData%2A> 方法提取 <xref:System.Windows.DataObject> 中的传输的数据并执行应用程序所需的任何数据处理。  <xref:System.Windows.DragDrop.Drop> 事件结束拖放操作。  
  
 下面的示例演示 <xref:System.Windows.Shapes.Ellipse> 元素的 <xref:System.Windows.DragDrop.Drop> 事件处理程序。  此代码应用拖放操作的效果，并且它类似于 <xref:System.Windows.DragDrop.DragEnter> 事件处理程序中的代码。  它会检查是否将 <xref:System.Windows.DataObject> 拖动到包含可以转换为 <xref:System.Windows.Media.Brush> 的字符串数据的椭圆上方。  如果是，将 <xref:System.Windows.Media.Brush> 应用于椭圆。  如果数据无法转换为 <xref:System.Windows.Media.Brush>，则不执行任何操作。  
  
 [!code-csharp[DragDropSnippets#Drop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#drop)]
 [!code-vb[DragDropSnippets#Drop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#drop)]  
  
## 请参阅  
 <xref:System.Windows.Clipboard>   
 [演练：对用户控件启用拖放功能](../../../../docs/framework/wpf/advanced/walkthrough-enabling-drag-and-drop-on-a-user-control.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/drag-and-drop-how-to-topics.md)   
 [拖放](../../../../docs/framework/wpf/advanced/drag-and-drop.md)