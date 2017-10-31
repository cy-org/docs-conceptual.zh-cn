---
title: "批注概述 | Microsoft Docs"
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
  - "文档, 批注"
  - "突出显示"
  - "便笺"
ms.assetid: 716bf474-29bd-4c74-84a4-8e0744bdad62
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 批注概述
在书面文档上写说明或注释是一件我们几乎认为理所当然的平常事。  这些说明或注释是在文档中添加的“批注”，用于标注信息或突出显示重要项，以便于将来参考。  尽管在打印文档上写注释很简单也很平常，但是在电子文档上添加个人注释却通常有很多的限制，且并不是在所有电子文档上都能添加个人注释。  
  
 本主题介绍了几种常见类型的批注，重点介绍便笺和突出显示，并举例说明 [!INCLUDE[TLA#tla_caf](../../../../includes/tlasharptla-caf-md.md)] 如何通过 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 文档查看控件简化这些类型的批注在应用程序中的使用。  支持批注的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 文档查看控件包括 <xref:System.Windows.Controls.FlowDocumentReader> 和 <xref:System.Windows.Controls.FlowDocumentScrollViewer>，以及从 <xref:System.Windows.Controls.Primitives.DocumentViewerBase> 派生的控件，如 <xref:System.Windows.Controls.DocumentViewer> 和 <xref:System.Windows.Controls.FlowDocumentPageViewer>。  
  
   
  
<a name="caf1_type_stickynotes"></a>   
## 便笺  
 典型的便笺包含在小块的彩色纸上书写的信息，之后这张彩色纸将“粘贴”到文档上。  数字便笺为电子文档提供类似的功能，但灵活性更高，可包括许多其他类型的内容，如键入文本、手写注释（如 [!INCLUDE[TLA#tla_tpc](../../../../includes/tlasharptla-tpc-md.md)]“墨迹”笔划）或 Web 链接。  
  
 下图显示了突出显示、文本便笺以及墨迹便笺批注的一些示例。  
  
 ![突出显示、文本和墨迹便笺批注。](../../../../docs/framework/wpf/advanced/media/caf-stickynote.jpg "CAF\_StickyNote")  
  
 下面的示例演示了可用来在应用程序中启用批注支持的方法。  
  
 [!code-csharp[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXml/CSharp/Window1.xaml.cs#docviewxmlstartannotations)]
 [!code-vb[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DocViewerAnnotationsXml/visualbasic/window1.xaml.vb#docviewxmlstartannotations)]  
  
<a name="caf1_type_callouts"></a>   
## 突出显示  
 当人们在书面文档上作标记时，往往使用创造性的方法来吸引他人对某些重要项的关注，这些方法有加下划线、突出显示、将句子中的个别字圈出来或者在空白的地方绘制标记或写注释。  [!INCLUDE[TLA#tla_caf](../../../../includes/tlasharptla-caf-md.md)] 中的突出显示批注具有类似的功能，用于标记显示在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 文档查看控件中的信息。  
  
 下图显示了突出显示批注的示例。  
  
 ![突出显示批注](../../../../docs/framework/wpf/advanced/media/caf-callouts.png "CAF\_Callouts")  
  
 用户通常以如下方法创建批注：首先选择一些文本或者关注的某一项，然后右击以显示批注选项的 <xref:System.Windows.Controls.ContextMenu>。  下面的示例演示了可用来声明包含路由命令的 <xref:System.Windows.Controls.ContextMenu> 的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，用户可以访问这些命令来创建和管理批注。  
  
 [!code-xml[DocViewerAnnotationsXps#CreateDeleteAnnotations](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXps/CSharp/Window1.xaml#createdeleteannotations)]  
  
<a name="caf1_framework_data_anchoring"></a>   
## 数据创作  
 [!INCLUDE[TLA2#tla_caf](../../../../includes/tla2sharptla-caf-md.md)] 将批注绑定到用户选择的数据，而不仅仅是绑定到显示视图上的某个位置。  因此，如果文档视图更改，例如，当用户滚动显示窗口或者调整其大小时，批注将仍然与所绑定到的选择数据捆绑在一起。  例如，下图显示了用户可以在选择文本上做的批注。  当文档视图更改（滚动、调整大小、缩放或者移动）时，突出显示批注将与最初选择的数据一起移动。  
  
 ![批注数据锚定](../../../../docs/framework/wpf/advanced/media/caf-dataanchoring.png "CAF\_DataAnchoring")  
  
<a name="matching_annotations_with_annotated_objects"></a>   
## 将批注与所批注的对象匹配  
 可以将批注与对应的批注对象匹配。  以一个具有注释窗格的简单文档读取器应用程序为例。  注释窗格可能是一个列表框，用于显示锚定到文档的批注列表中的文本。  如果用户在列表框中选择一项，则应用程序将显示相应的批注对象所锚定到的文档段落。  
  
 下面的示例演示如何实现充当注释窗格的列表框的事件处理程序。  
  
 [!code-csharp[FlowDocumentAnnotatedViewer#Handler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/CSharp/Window1.xaml.cs#handler)]
 [!code-vb[FlowDocumentAnnotatedViewer#Handler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/visualbasic/window1.xaml.vb#handler)]  
  
 另一示例方案涉及通过电子邮件实现文档读取器之间批注和便笺的交换的应用程序。  此功能使这些应用程序可以将读取器导航到包含要交换的批注的页面。  
  
## 请参阅  
 <xref:System.Windows.Controls.Primitives.DocumentViewerBase>   
 <xref:System.Windows.Controls.DocumentViewer>   
 <xref:System.Windows.Controls.FlowDocumentPageViewer>   
 <xref:System.Windows.Controls.FlowDocumentScrollViewer>   
 <xref:System.Windows.Controls.FlowDocumentReader>   
 <xref:System.Windows.Annotations.IAnchorInfo>   
 [批注架构](../../../../docs/framework/wpf/advanced/annotations-schema.md)   
 [ContextMenu 概述](../../../../docs/framework/wpf/controls/contextmenu-overview.md)   
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)   
 [流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [How to: Add a Command to a MenuItem](http://msdn.microsoft.com/zh-cn/013d68a0-5373-4a68-bd91-5de574307370)