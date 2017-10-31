---
title: "如何：以编程方式打印 XPS 文件 | Microsoft Docs"
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
  - "以编程方式打印 XPS 文件"
  - "XPS 文件, 以编程方式打印"
ms.assetid: 0b1c0a3f-b19e-43d6-bcc9-eb3ec4e555ad
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：以编程方式打印 XPS 文件
可以使用 <xref:System.Printing.PrintQueue.AddJob%2A> 方法的一个重载来打印 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 文件，而不必打开 <xref:System.Windows.Controls.PrintDialog>，或者从原则上来说，根本不必打开任何[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。  
  
 您还可以使用 <xref:System.Windows.Xps.XpsDocumentWriter> 的许多 <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> 和 <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> 方法来打印 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 文件。  有关更多信息，请参见[Printing an XPS Document](http://msdn.microsoft.com/zh-cn/849555c8-0c4e-48c0-86bc-a5494c69b36c)。  
  
 打印 [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] 的另一种方法是使用 <xref:System.Windows.Controls.PrintDialog> 控件的 <xref:System.Windows.Controls.PrintDialog.PrintDocument%2A> 或 <xref:System.Windows.Controls.PrintDialog.PrintVisual%2A> 方法。  请参见[调用打印对话框](../../../../docs/framework/wpf/advanced/how-to-invoke-a-print-dialog.md)。  
  
## 示例  
 使用三参数 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 方法的主要步骤如下。  下面的示例给出了详细信息。  
  
1.  确定打印机是否是 XPSDrv 打印机  （有关 XPSDrv 的更多信息，请参见[打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)）。  
  
2.  如果打印机不是 XPSDrv 打印机，将线程的单元设置为单线程。  
  
3.  实例化一个打印服务器和打印队列对象。  
  
4.  调用该方法，并指定作业名称、要打印的文件以及指示打印机是否是 XPSDrv 打印机的 <xref:System.Boolean> 标志。  
  
 下面的示例演示如何以批处理方式打印一个目录中的所有 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文件。  尽管应用程序提示用户指定目录，但是三参数的 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 方法不需要[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。  它可以用在可传递给它的 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文件名和路径所在的任何代码路径中。  
  
 只要 <xref:System.Boolean> 参数是 `false`（当使用的不是 XPSDrv 打印机时，该参数必须为此值），<xref:System.Printing.PrintQueue.AddJob%2A> 的三参数 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 重载就必须运行在单个线程单元中。  但是，[!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] 的默认单元状态是多线程。  必须将此默认设置反过来，因为本示例采用的不是 XPSDrv 打印机。  
  
 有两种方法来更改默认设置。  一种方法是在应用程序的 `Main` 方法的第一行（通常是“`static void Main(string[] args)`”）的紧上方添加 <xref:System.STAThreadAttribute>（即“`[System.STAThreadAttribute()]`”）。  但是，许多应用程序都要求 `Main` 方法有多线程单元状态，因此存在第二种方法，即：在一个单独的线程中放置对 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 的调用，该线程的单元状态通过 <xref:System.Threading.Thread.SetApartmentState%2A> 设置为 <xref:System.Threading.ApartmentState>。  下面的示例使用第二种方法。  
  
 因此，示例的开头实例化一个 <xref:System.Threading.Thread> 对象，并将一个 **PrintXPS** 方法作为 <xref:System.Threading.ThreadStart> 参数传递给它  （**PrintXPS** 方法在本示例的稍后部分定义）。接下来，线程设置为单线程单元。  `Main` 方法的剩余代码启动新线程。  
  
 该示例的主要内容在 `static` **BatchXPSPrinter.PrintXPS** 方法中。  在创建打印服务器和队列后，该方法会提示用户输入包含 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文件的目录。  在确认该目录存在并且其中存在 \*.xps 文件后，该方法将每个这样的文件添加到打印队列中。  该示例假定打印机不是 XPSDrv，因此我们将 `false` 传递给 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 方法的最后一个参数。  为此，该方法在尝试将文件转换为打印机的页面描述语言之前，会先验证文件中的 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 标记。  如果验证失败，将引发一个异常。  代码示例将捕捉此异常，将有关此异常的信息通知给用户，然后继续处理下一个 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文件。  
  
 [!code-csharp[BatchPrintXPSFiles#BatchPrintXPSFiles](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BatchPrintXPSFiles/CSharp/Program.cs#batchprintxpsfiles)]
 [!code-vb[BatchPrintXPSFiles#BatchPrintXPSFiles](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BatchPrintXPSFiles/visualbasic/program.vb#batchprintxpsfiles)]  
  
 如果您使用的是 XPSDrv 打印机，则可以将最后一个参数设置为 `true`。  在这种情况下，因为 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 是打印机的页面描述语言，所以此方法会将文件发送到打印机，而不对它进行验证或将它转换为另一种页面描述语言。  如果您在设计时不确定应用程序是否将使用 XPSDrv 打印机，则可以修改应用程序，使它读取 <xref:System.Printing.PrintQueue.IsXpsDevice%2A> 属性，并根据它找到的内容进行分支。  
  
 因为在 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] 和 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] 发行之后，最初几乎没有 XPSDrv 打印机可以立即投入使用，因此，可能需要将非 XPSDrv 打印机假装成 XPSDrv 打印机。  为此，应将 Pipelineconfig.xml 添加到运行您的应用程序的计算机的以下注册表项中的文件列表：  
  
 HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Print\\Environments\\Windows NT x86\\Drivers\\Version\-3\\*\<PseudoXPSPrinter\>*\\DependentFiles  
  
 其中 *\<PseudoXPSPrinter\>* 是任一打印队列。  然后必须重新启动计算机。  
  
 这种假装使您可以将 `true` 作为 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 的最后一个参数来传递，而不会导致异常，但因为 *\<PseudoXPSPrinter\>* 并不是真正的 XPSDrv 打印机，因此打印出来的将仅仅是乱码。  
  
 **注意** 为简单起见，上面的示例通过检查是否存在扩展名 \*.xps 来检测文件是否是 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)]。  但是，[!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 文件不一定有此扩展名。  [isXPS.exe（isXPS 合规性工具）](../Topic/isXPS.exe%20\(isXPS%20Conformance%20Tool\).md) 也是一种测试文件是否是 [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] 的方法。  
  
## 请参阅  
 <xref:System.Printing.PrintQueue>   
 <xref:System.Printing.PrintQueue.AddJob%2A>   
 <xref:System.Threading.ApartmentState>   
 <xref:System.STAThreadAttribute>   
 [XPS](http://www.microsoft.com/xps)   
 [Printing an XPS Document](http://msdn.microsoft.com/zh-cn/849555c8-0c4e-48c0-86bc-a5494c69b36c)   
 [Managed and Unmanaged Threading](http://msdn.microsoft.com/zh-cn/db425c20-4b2f-4433-bf96-76071c7881e5)   
 [isXPS.exe（isXPS 合规性工具）](../Topic/isXPS.exe%20\(isXPS%20Conformance%20Tool\).md)   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)