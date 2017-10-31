---
title: "TextBox 概述 | Microsoft Docs"
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
  - "控件, 文本框"
  - "TextBox 控件, 关于 TextBox 控件"
ms.assetid: 1ba6dc5b-11a7-4247-9213-36c6729ee35f
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# TextBox 概述
使用 <xref:System.Windows.Controls.TextBox> 类可以显示或编辑非格式化文本。  <xref:System.Windows.Controls.TextBox> 的常用用途是在表单中编辑非格式化文本。  例如，如果一个表单要求输入用户姓名、电话号码等，则可以使用 <xref:System.Windows.Controls.TextBox> 控件来进行文本输入。  本主题介绍 <xref:System.Windows.Controls.TextBox> 类，并提供如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 和 [!INCLUDE[TLA#tla_lhcshrp](../../../../includes/tlasharptla-lhcshrp-md.md)] 中使用它的示例。  
  
   
  
<a name="textbox_or_richtextbox"></a>   
## 使用 TextBox 还是 RichTextBox？  
 <xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.RichTextBox> 都允许用户输入文本，但是这两个控件用于不同的情形。  <xref:System.Windows.Controls.TextBox> 要求的系统资源比 <xref:System.Windows.Controls.RichTextBox> 少，因此当只需编辑纯文本（即用于表单）时，它是理想选择。  当用户需要编辑已设置格式的文本、图像、表或其他支持的内容时，最好选择 <xref:System.Windows.Controls.RichTextBox>。  例如，编辑需要格式、图像等内容的文档、文章或博客时，最好使用 <xref:System.Windows.Controls.RichTextBox>。  下表汇总了 <xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.TextBox> 的主要功能。  
  
|控件|实时拼写检查|上下文菜单|格式设置命令，例如 <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> \(Ctr\+B\)|<xref:System.Windows.Documents.FlowDocument> 内容，例如图像、段落、表等。|  
|--------|------------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.TextBox>|是|是|否|不能。|  
|<xref:System.Windows.Controls.RichTextBox>|是|是|是（请参见 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)）|是（请参见 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)）|  
  
> [!NOTE]
>  虽然 <xref:System.Windows.Controls.TextBox> 不支持 <xref:System.Windows.Documents.EditingCommands.ToggleBold%2A> \(Ctr\+B\) 之类的与格式设置有关的编辑命令，但是这两个控件都支持许多基本命令，例如 <xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A>。  有关更多信息，请参见 <xref:System.Windows.Documents.EditingCommands>。  
  
 下面几节介绍了 <xref:System.Windows.Controls.TextBox> 支持的功能。  有关 <xref:System.Windows.Controls.RichTextBox>的更多信息，请参见[RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)。  
  
### 实时拼写检查  
 您可以在 <xref:System.Windows.Controls.TextBox> 或 <xref:System.Windows.Controls.RichTextBox> 中启用实时拼写检查。  启用拼写检查后，会在所有拼写有误的字词下面显示红线（请见下图）。  
  
 ![具有拼写检查功能的 TextBox](../../../../docs/framework/wpf/controls/media/editing-textbox-with-spellchecking.png "Editing\_TextBox\_with\_Spellchecking")  
  
 若要了解如何启用拼写检查，请参见[在文本编辑控件中启用拼写检查](../../../../docs/framework/wpf/controls/how-to-enable-spell-checking-in-a-text-editing-control.md)。  
  
### 上下文菜单  
 默认情况下，<xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.RichTextBox> 都会在用户在右击该控件时显示一个上下文菜单。  用户可以使用该上下文菜单进行剪切、复制或粘贴（请见下图）。  
  
 ![具有上下文菜单的 TextBox](../../../../docs/framework/wpf/controls/media/editing-textbox-with-context-menu.png "Editing\_TextBox\_with\_Context\_Menu")  
  
 您可以创建自己的自定义上下文菜单来重写默认行为。  有关更多信息，请参见[通过 TextBox 使用自定义上下文菜单](../../../../docs/framework/wpf/controls/how-to-use-a-custom-context-menu-with-a-textbox.md)。  
  
<a name="creating_textboxes"></a>   
## 创建 TextBox  
 <xref:System.Windows.Controls.TextBox> 的高度可以是一行，也可以包含多行。  对于输入少量纯文本（例如表单中的“姓名”、“电话号码”等）而言，单行 <xref:System.Windows.Controls.TextBox> 是  最好的  选择。  下面的示例演示如何创建一个单行 <xref:System.Windows.Controls.TextBox>。  
  
 [!code-xml[TextBoxMiscSnippets_snip#BasicTextBoxExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/basictextboxexample.xaml#basictextboxexamplewholepage)]  
  
 您还可以创建一个使用户可以输入多行文本的 <xref:System.Windows.Controls.TextBox>。  例如，如果您的表单要求输入用户的自传，您可能需要使用支持多行文本的 <xref:System.Windows.Controls.TextBox>。  下面的示例演示如何使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 来定义一个 <xref:System.Windows.Controls.TextBox> 控件，该控件可自动扩展以容纳多行文本。  
  
 [!code-xml[TextBox_MiscCode#_MultilineTextBoxXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
 将 <xref:System.Windows.Controls.TextBox.TextWrapping%2A> 特性设置为 `Wrap` 会导致文本在到达 <xref:System.Windows.Controls.TextBox> 控件的边缘时换至新行，必要时会自动扩展 <xref:System.Windows.Controls.TextBox> 控件以便为新行留出空间。  
  
 将 <xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A> 特性设置为 `true` 会导致在按 Return 键时插入新行，必要时会再次自动扩展 <xref:System.Windows.Controls.TextBox> 以便为新行留出空间。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A> 特性向 <xref:System.Windows.Controls.TextBox> 添加一个滚动条，以便在 <xref:System.Windows.Controls.TextBox> 超出包含它的框架或窗口的大小时，可以滚动 <xref:System.Windows.Controls.TextBox> 的内容。  
  
 有关与使用 <xref:System.Windows.Controls.TextBox> 关联的不同任务的更多信息，请参见 [帮助主题](../../../../docs/framework/wpf/controls/textbox-how-to-topics.md)。  
  
<a name="editing_commands"></a>   
## 在内容更改时进行检测  
 通常，只要 <xref:System.Windows.Controls.TextBox> 或 <xref:System.Windows.Controls.RichTextBox> 中的文本发生更改，就应使用 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 事件进行检测，而不像您可能认为的那样使用 <xref:System.Windows.UIElement.KeyDown>。  有关示例，请参见 [检测 TextBox 中的文本何时更改](../../../../docs/framework/wpf/controls/how-to-detect-when-text-in-a-textbox-has-changed.md)。  
  
## 请参阅  
 [帮助主题](../../../../docs/framework/wpf/controls/textbox-how-to-topics.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)