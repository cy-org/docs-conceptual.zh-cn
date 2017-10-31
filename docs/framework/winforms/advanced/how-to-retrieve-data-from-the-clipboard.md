---
title: "如何：从剪贴板检索数据 | Microsoft Docs"
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
  - "剪贴板, 检索数据"
  - "粘贴剪贴板数据"
ms.assetid: 99612537-2c8a-449f-aab5-2b3b28d656e7
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：从剪贴板检索数据
<xref:System.Windows.Forms.Clipboard> 类提供了可以用来与 Windows 操作系统剪贴板功能交互的方法。  许多应用程序都将剪贴板用作一个临时数据储存库。  例如，字处理器在剪切和粘贴操作期间使用剪贴板。  剪贴板还可用来从一个应用程序向另一个应用程序传输信息。  
  
 某些应用程序可以在剪贴板上以多种格式存储数据，这样增加了可能使用该数据的其他应用程序的数量。  剪贴板格式是一个用于标识格式的字符串。  使用已标识格式的应用程序可以在剪贴板中检索关联的数据。  <xref:System.Windows.Forms.DataFormats> 类提供了预定义的格式名称以方便您使用。  您也可以使用您自己的格式名称，或使用某对象的类型作为其格式。  有关向剪贴板添加数据的信息，请参见 [如何：将数据添加到剪贴板](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)。  
  
 若要确定剪贴板是否包含特定格式的数据，请使用 `Contains`*格式* 方法之一或 <xref:System.Windows.Forms.Clipboard.GetData%2A> 方法。  若要从剪贴板检索数据，请使用 `Get`*格式* 方法之一或 <xref:System.Windows.Forms.Clipboard.GetData%2A> 方法。  这些方法是 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中的新方法。  
  
 若要使用 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] 之前的版本访问剪贴板中的数据，请使用 <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> 方法，并调用返回的 <xref:System.Windows.Forms.IDataObject> 的方法。  例如，若要确定某个特定格式在返回对象中是否可用，请调用 <xref:System.Windows.Forms.IDataObject.GetDataPresent%2A> 方法。  
  
> [!NOTE]
>  所有基于 Windows 的应用程序都共享系统剪贴板。  因此，当您切换到另一个应用程序时，其内容也会发生更改。  
>   
>  <xref:System.Windows.Forms.Clipboard> 类只能在设置为单线程单元 \(STA\) 模式的线程中使用。  若要使用此类，请确保您的 `Main` 方法已用 <xref:System.STAThreadAttribute> 特性标记。  
  
### 检索剪贴板中单一通用格式的数据  
  
1.  使用 <xref:System.Windows.Forms.Clipboard.GetAudioStream%2A>、<xref:System.Windows.Forms.Clipboard.GetFileDropList%2A>、<xref:System.Windows.Forms.Clipboard.GetImage%2A> 或 <xref:System.Windows.Forms.Clipboard.GetText%2A> 方法。  还可以选择先使用相应的 `Contains`*格式* 方法来确定数据在特定格式下是否可用。  这些方法只在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中可用。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]  
  
### 检索剪贴板中自定义格式的数据  
  
1.  使用具有自定义格式名称的 <xref:System.Windows.Forms.Clipboard.GetData%2A> 方法。  此方法只在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中可用。  
  
     您还可以在使用 <xref:System.Windows.Forms.Clipboard.SetData%2A> 方法时使用预定义的格式名称。  有关更多信息，请参见 <xref:System.Windows.Forms.DataFormats>。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
### 检索剪贴板中多种格式的数据  
  
1.  请使用 <xref:System.Windows.Forms.Clipboard.GetDataObject%2A> 方法。  在 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] 的早期版本中，必须使用此方法才能检索剪贴板中的数据。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
## 请参阅  
 [拖放操作和剪贴板支持](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)   
 [如何：将数据添加到剪贴板](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)