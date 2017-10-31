---
title: "如何：在应用程序之间执行拖放操作 | Microsoft Docs"
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
  - "拖放, 在应用程序之间"
ms.assetid: fa347436-2b12-4dd6-8507-59d7241f6a06
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在应用程序之间执行拖放操作
执行应用程序间的拖放操作与在一个应用程序内启用此操作并无差别，只要涉及的两个应用程序均按照 <xref:System.Windows.Forms.DragEventArgs.AllowedEffect%2A> 和 <xref:System.Windows.Forms.DragEventArgs.Effect%2A> 属性之间建立的“协定”实施行为。  
  
 在下面的过程中，你将使用你创建的基于 Windows 的应用程序和 Windows 操作系统附带的“写字板”字处理器，以在应用程序之间执行拖放操作。  写字板具有一组特定的用于被拖放文本的允许的效果；你要为其编写代码的基于 Windows 的应用程序将使用这些效果来成功地完成拖放操作。  
  
### 在应用程序之间执行拖放操作  
  
1.  创建新的 Windows 窗体应用程序。  
  
2.  向窗体添加一个 <xref:System.Windows.Forms.TextBox> 控件。  
  
3.  配置 <xref:System.Windows.Forms.TextBox> 控件以接收放置的数据。  
  
     有关详细信息，请参阅[演练：在 Windows 窗体中执行拖放操作](../../../../docs/framework/winforms/advanced/walkthrough-performing-a-drag-and-drop-operation-in-windows-forms.md)。  
  
4.  运行基于 Windows 的应用程序，并在运行该应用程序时运行写字板。  
  
     写字板是由 Windows 安装的允许拖放操作的文本编辑器。  可以通过按“启动”按钮，选择“运行”，在“运行”对话框的文本框中键入 `WordPad`，然后单击“确定”来访问它。  
  
5.  打开写字板后，在其中键入文本字符串。  
  
6.  使用鼠标选择该文本，然后将所选的文本拖动到基于 Windows 的应用程序中的 <xref:System.Windows.Forms.TextBox> 控件之上。  
  
     注意，当你将鼠标移到 <xref:System.Windows.Forms.TextBox> 控件上（并因此引发 <xref:System.Windows.Forms.Control.DragEnter> 事件）时，光标会改变，可以将所选的文本放入 <xref:System.Windows.Forms.TextBox> 控件。  
  
     此外，还可以配置 <xref:System.Windows.Forms.TextBox> 控件，以允许将文本字符串拖放到写字板中。  有关详细信息，请参阅[演练：在 Windows 窗体中执行拖放操作](../../../../docs/framework/winforms/advanced/walkthrough-performing-a-drag-and-drop-operation-in-windows-forms.md)。  
  
## 请参阅  
 [如何：将数据添加到剪贴板](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)   
 [如何：从剪贴板检索数据](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)   
 [拖放操作和剪贴板支持](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)