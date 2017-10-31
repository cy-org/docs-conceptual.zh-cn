---
title: "RichTextBox 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件, RichTextBox"
  - "RichTextBox 控件 [WPF], 关于 RichTextBox 控件"
ms.assetid: c94548b2-c1e9-4b62-b10c-dd8740eb23d8
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# RichTextBox 概述
使用 <xref:System.Windows.Controls.RichTextBox> 控件，可以显示或编辑流内容（包括段落、图像、表等）。  本主题介绍 <xref:System.Windows.Controls.TextBox> 类，并提供如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 和 [!INCLUDE[TLA#tla_lhcshrp](../../../../includes/tlasharptla-lhcshrp-md.md)] 中使用它的示例。  
  
   
  
<a name="textbox_or_richtextbox"></a>   
## 使用 TextBox 还是 RichTextBox？  
 <xref:System.Windows.Controls.RichTextBox> 和 <xref:System.Windows.Controls.TextBox> 都允许用户编辑文本，但是这两个控件用于不同的情形。  当用户需要编辑带格式的文本、图像、表或其他丰富内容时，最好选择 <xref:System.Windows.Controls.RichTextBox>。  例如，编辑需要格式、图像等内容的文档、文章或博客时，最好使用 <xref:System.Windows.Controls.RichTextBox>。  <xref:System.Windows.Controls.TextBox> 要求的系统资源比 <xref:System.Windows.Controls.RichTextBox> 少，因此当只需编辑纯文本（即  用于窗体）时，它是理想选择。  有关 <xref:System.Windows.Controls.TextBox> 的更多信息，请参见 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)。  下表汇总了 <xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.RichTextBox> 的主要功能。  
  
|控件|实时拼写检查|上下文菜单|格式设置命令，例如 <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> \(Ctr\+B\)|<xref:System.Windows.Documents.FlowDocument> 内容，例如图像、段落、表等。|  
|--------|------------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.TextBox>|是|是|否|不能。|  
|<xref:System.Windows.Controls.RichTextBox>|是|是|是|是|  
  
 **注意：**尽管 <xref:System.Windows.Controls.TextBox> 不支持与格式设置有关的命令，如 <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> \(Ctr\+B\)，但是这两个控件都支持许多基本命令，如 <xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A>）。  
  
 后面将更详细地介绍上表中的功能。  
  
<a name="creating_a_richtextbox"></a>   
## 创建 RichTextBox  
 下面的代码演示如何创建可供用户在其中编辑丰富内容的 <xref:System.Windows.Controls.RichTextBox>。  
  
 [!code-xml[RichTextBoxMiscSnippets_snip#BasicRichTextBoxExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/BasicRichTextBoxExample.xaml#basicrichtextboxexamplewholepage)]  
  
 具体来说，在 <xref:System.Windows.Controls.RichTextBox> 编辑的内容是流内容。  流内容中可以包含许多类型的元素（包括带格式的文本、图像、列表和表）。  有关流文档的详细信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)。  为了包含流内容，可以让 <xref:System.Windows.Controls.RichTextBox> 承载一个 <xref:System.Windows.Documents.FlowDocument> 对象，该对象中同样包含可编辑的内容。  为了演示 <xref:System.Windows.Controls.RichTextBox> 中的流内容，下面的代码演示如何创建具有一个段落和一些加粗文本的 <xref:System.Windows.Controls.RichTextBox>。  
  
 [!code-xml[RichTextBoxMiscSnippets_snip#RichTextBoxWithContentExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/RichTextBoxWithContentExample.xaml#richtextboxwithcontentexamplewholepage)]  
  
 [!code-csharp[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/CSharp/BasicRichTextBoxWithContentExample.cs#basicrichtextboxwithcontentcodeonlyexample)]
 [!code-vb[RichTextBoxMiscSnippets_procedural_snip#BasicRichTextBoxWithContentCodeOnlyExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_procedural_snip/visualbasic/basicrichtextboxwithcontentexample.vb#basicrichtextboxwithcontentcodeonlyexample)]  
  
 下图显示的是此示例的呈现效果。  
  
 ![具有内容的 RichTextBox](../../../../docs/framework/wpf/controls/media/editing-richtextbox-with-content.png "Editing\_RichTextBox\_with\_Content")  
  
 内容在 <xref:System.Windows.Controls.RichTextBox> 中的显示方式由 <xref:System.Windows.Documents.Paragraph> 和 <xref:System.Windows.Documents.Bold> 之类的元素确定。  当用户编辑 <xref:System.Windows.Controls.RichTextBox> 内容时，这些元素会改变此流内容。  有关流内容的功能及其工作方式的更多信息，请参见[流文档概述](../../../../docs/framework/wpf/advanced/flow-document-overview.md)。  
  
 **注意：** <xref:System.Windows.Controls.RichTextBox> 内部的流内容的行为并不与其他控件中包含的流内容完全相同。  例如，在 <xref:System.Windows.Controls.RichTextBox> 中不分栏，因此没有自动调整大小行为。  另外，在 <xref:System.Windows.Controls.RichTextBox> 中不能使用内置功能（如搜索、查看模式、页面导航和缩放）。  
  
<a name="realtime_spellechecking"></a>   
## 实时拼写检查  
 您可以在 <xref:System.Windows.Controls.TextBox> 或 <xref:System.Windows.Controls.RichTextBox> 中启用实时拼写检查。  启用拼写检查后，会在所有拼写有误的字词下面显示红线（请见下图）。  
  
 ![具有拼写检查功能的 TextBox](../../../../docs/framework/wpf/controls/media/editing-textbox-with-spellchecking.png "Editing\_TextBox\_with\_Spellchecking")  
  
 若要了解如何启用拼写检查，请参见[在文本编辑控件中启用拼写检查](../../../../docs/framework/wpf/controls/how-to-enable-spell-checking-in-a-text-editing-control.md)。  
  
<a name="context_menu"></a>   
## 上下文菜单  
 默认情况下，<xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.RichTextBox> 都会在用户在右击该控件时显示一个上下文菜单。  用户可以使用上下文菜单进行剪切、复制或粘贴（请见下图）。  
  
 ![具有上下文菜单的 TextBox](../../../../docs/framework/wpf/controls/media/editing-textbox-with-context-menu.png "Editing\_TextBox\_with\_Context\_Menu")  
  
 您可以创建自己的自定义上下文菜单来重写默认行为。  有关更多信息，请参见[在 RichTextBox 中定位自定义上下文菜单](../../../../docs/framework/wpf/controls/how-to-position-a-custom-context-menu-in-a-richtextbox.md)。  
  
<a name="detect_when_content_changes"></a>   
## 编辑命令  
 用户可以使用编辑命令来为 <xref:System.Windows.Controls.RichTextBox> 中的可编辑内容设置格式。  除了基本编辑命令外，<xref:System.Windows.Controls.RichTextBox> 还包括 <xref:System.Windows.Controls.TextBox> 不支持的格式化命令。  例如，当在 <xref:System.Windows.Controls.RichTextBox> 中进行编辑时，用户可以按 Ctr\+B 来切换加粗文本的格式设置。  有关可用命令的完整列表，请参见 <xref:System.Windows.Documents.EditingCommands>。  除了使用键盘快捷键以外，您还可以将命令挂钩到其他控件（如按钮）。  下面的示例演示如何创建简单的工具栏，其中包含用户可用来更改文本格式的按钮。  
  
 [!code-xml[RichTextBox_InputPanel_snip#RichTextBoxWithToolBarExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_InputPanel_snip/CS/Window1.xaml#richtextboxwithtoolbarexamplewholepage)]  
  
 下图显示的是此示例的显示效果。  
  
 ![具有工具栏的 RichTextBox](../../../../docs/framework/wpf/controls/media/editing-richtextbox-with-toobar.png "Editing\_RichTextBox\_with\_TooBar")  
  
<a name="editing_commands"></a>   
## 在内容更改时进行检测  
 通常，只要 <xref:System.Windows.Controls.TextBox> 或 <xref:System.Windows.Controls.RichTextBox> 中的文本发生更改，就应使用 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 事件进行检测，而不是像您可能预期的那样使用 <xref:System.Windows.UIElement.KeyDown>。  有关示例，请参见 [检测 TextBox 中的文本何时更改](../../../../docs/framework/wpf/controls/how-to-detect-when-text-in-a-textbox-has-changed.md)。  
  
<a name="save_load_and_print_richtextbox_content"></a>   
## 保存、加载和打印 RichTextBox 内容  
 下面的示例演示如何将 <xref:System.Windows.Controls.RichTextBox> 的内容保存到文件、如何将该内容重新加载到 <xref:System.Windows.Controls.RichTextBox> 中以及如何打印这些内容。  下面是该示例的标记。  
  
 [!code-xml[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml#saveloadprintrtbexamplewholepage)]  
  
 下面是该示例的隐藏代码。  
  
 [!code-csharp[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/CSharp/SaveLoadPrintRTB.xaml.cs#saveloadprintrtbcodeexamplewholepage)]
 [!code-vb[RichTextBoxMiscSnippets_snip#SaveLoadPrintRTBCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBoxMiscSnippets_snip/VisualBasic/SaveLoadPrintRTB.xaml.vb#saveloadprintrtbcodeexamplewholepage)]  
  
## 请参阅  
 [帮助主题](../../../../docs/framework/wpf/controls/richtextbox-how-to-topics.md)   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)