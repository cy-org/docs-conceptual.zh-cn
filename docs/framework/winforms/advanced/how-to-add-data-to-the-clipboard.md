---
title: "如何：将数据添加到剪贴板 | Microsoft Docs"
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
  - "剪贴板, 将数据复制到"
  - "数据 [Windows 窗体], 复制到剪贴板"
ms.assetid: 25152454-0e78-40a9-8a9e-a2a5a274e517
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：将数据添加到剪贴板
<xref:System.Windows.Forms.Clipboard> 类提供了可以用来与 Windows 操作系统剪贴板功能交互的方法。  许多应用程序都将剪贴板用作一个临时数据储存库。  例如，字处理器在剪切和粘贴操作期间使用剪贴板。  剪贴板还可用于从一个应用程序向另一个应用程序传输数据。  
  
 向剪贴板添加数据时，可以指示数据格式，以便在其他应用程序能够使用该格式时可以识别该数据。  还可以按多种不同的格式将数据添加到剪贴板，这样增加了有可能使用该数据的其他应用程序的数量。  
  
 剪贴板格式是一个字符串，用于标识格式，以便使用该格式的应用程序可以检索关联的数据。  <xref:System.Windows.Forms.DataFormats> 类提供了预定义的格式名称以方便您使用。  您也可以使用您自己的格式名称，或将对象的类型用作其格式名称。  
  
 若要以一种或多种格式将数据添加到剪贴板，请使用 <xref:System.Windows.Forms.Clipboard.SetDataObject%2A> 方法。  可以将任意对象传递给此方法，但若要以多种格式添加数据，必须首先将数据添加到一个专门用于多种格式的单独对象中。  通常，应当将数据添加到 <xref:System.Windows.Forms.DataObject> 中，但可以使用任何实现了 <xref:System.Windows.Forms.IDataObject> 接口的类型。  
  
 在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]中，可以使用为使基本的剪贴板任务更容易执行而设计的新方法，将数据直接添加到剪贴板中。  以单一的常用格式（如文本）处理数据时，可以使用这些方法。  
  
> [!NOTE]
>  所有基于 Windows 的应用程序都共享剪贴板。  因此，当您切换到另一个应用程序时，其内容也会发生更改。  
>   
>  <xref:System.Windows.Forms.Clipboard> 类只能在设置为单线程单元 \(STA\) 模式的线程中使用。  若要使用此类，请确保您的 `Main` 方法已用 <xref:System.STAThreadAttribute> 特性标记它。  
>   
>  对象必须是可序列化的，才能将它放在剪贴板上。  若要使类型可序列化，请用 <xref:System.SerializableAttribute> 特性标记它。  如果将非可序列化对象传递给剪贴板方法，则该方法将失败，而且不会引发异常。  有关序列化的更多信息，请参见 <xref:System.Runtime.Serialization>。  
  
### 将数据以单一常用格式添加到剪贴板上  
  
1.  使用 <xref:System.Windows.Forms.Clipboard.SetAudio%2A>、<xref:System.Windows.Forms.Clipboard.SetFileDropList%2A>、<xref:System.Windows.Forms.Clipboard.SetImage%2A> 或 <xref:System.Windows.Forms.Clipboard.SetText%2A> 方法。  这些方法只在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中可用。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.Clipboard#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#2)]  
  
### 将数据以自定义格式添加到剪贴板中  
  
1.  使用具有自定义格式名称的 <xref:System.Windows.Forms.Clipboard.SetData%2A> 方法。  此方法只在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中可用。  
  
     您还可以在使用 <xref:System.Windows.Forms.Clipboard.SetData%2A> 方法时使用预定义的格式名称。  有关更多信息，请参见 <xref:System.Windows.Forms.DataFormats>。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.Clipboard#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#3)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
### 将数据以多种格式添加到剪贴板上  
  
1.  使用 <xref:System.Windows.Forms.Clipboard.SetDataObject%2A> 方法，并传入包含数据的 <xref:System.Windows.Forms.DataObject>。  在 [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)] 的早期版本中，必须使用此方法才能向剪贴板添加数据。  
  
     [!code-csharp[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.Clipboard#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#4)]  
    [!code-csharp[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/CS/form1.cs#100)]
    [!code-vb[System.Windows.Forms.Clipboard#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Clipboard/vb/form1.vb#100)]  
  
## 请参阅  
 [拖放操作和剪贴板支持](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)   
 [如何：从剪贴板检索数据](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)