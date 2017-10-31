---
title: "如何：调用打印对话框 | Microsoft Docs"
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
  - "调用打印对话框"
  - "打印对话框, 调用"
ms.assetid: e3a2c84c-74fe-45a4-8501-5813f9dbfed2
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：调用打印对话框
若要提供从应用程序打印的功能，您只需创建并打开 <xref:System.Windows.Controls.PrintDialog> 对象。  
  
## 示例  
 <xref:System.Windows.Controls.PrintDialog> 控件为 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]、配置和 [!INCLUDE[TLA2#tla_metro](../../../../includes/tla2sharptla-metro-md.md)] 作业提交提供单入口点。  此控件易于使用，并且可以通过使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 标记或代码进行实例化。  下面的示例演示如何在代码中实例化和打开控件并从中进行打印，  以及如何确保对话框为用户提供设置特定打印页数范围的选项。  此代码示例假定在 C: 驱动器的根目录下有一个名为 FixedDocumentSequence.xps 的文件。  
  
 [!code-csharp[printdialog#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PrintDialog/CSharp/Window1.xaml.cs#1)]
 [!code-vb[printdialog#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PrintDialog/visualbasic/window1.xaml.vb#1)]  
  
 一旦打开此对话框，用户即可从其计算机上安装的打印机中进行选择。  他们还可以选择 [Microsoft XPS Document Writer](http://go.microsoft.com/fwlink/?LinkId=147319) 来创建 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 文件而非打印作业。  
  
> [!NOTE]
>  请不要将本主题所讨论的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的 <xref:System.Windows.Controls.PrintDialog?displayProperty=fullName> 控件与 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]的 <xref:System.Windows.Forms.PrintDialog?displayProperty=fullName> 组件混淆。  
  
 严格来说，可以使用 <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> 方法而根本无需打开此对话框。  因此，可以将控件作为看不见的打印组件使用。  但由于性能原因，最好使用 <xref:System.Printing.PrintQueue.AddJob%2A> 方法或 <xref:System.Windows.Xps.XpsDocumentWriter> 的多个 <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> 和 <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> 方法之一。  有关更多信息，请参见[以编程方式打印 XPS 文件](../../../../docs/framework/wpf/advanced/how-to-programmatically-print-xps-files.md)和[Printing an XPS Document](http://msdn.microsoft.com/zh-cn/849555c8-0c4e-48c0-86bc-a5494c69b36c)。  
  
## 请参阅  
 <xref:System.Windows.Controls.PrintDialog>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Microsoft XPS Document Writer](http://go.microsoft.com/fwlink/?LinkId=147319)