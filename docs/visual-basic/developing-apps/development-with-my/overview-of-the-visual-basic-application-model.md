---
title: "Visual Basic 应用程序模型概述 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My.Application object, Visual Basic application model
- Visual Basic application model
ms.assetid: 17538984-84fe-43c9-82c8-724c9529fe8b
caps.latest.revision: 30
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0925bb102c148480d82128b91cbf1762de24e7ec
ms.lasthandoff: 03/13/2017

---
# <a name="overview-of-the-visual-basic-application-model"></a>Visual Basic 应用程序模型概述
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供用于控制 Windows 窗体应用程序的行为的定义完善的模型︰[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]应用程序模型。 此模型包含用于处理应用程序的启动和关闭，以及用于捕获的未经处理异常的事件。 它还提供用于开发单实例应用程序的支持。 应用程序模型是可扩展的，因此需要更多控制的开发人员可以自定义其可重写方法。  
  
## <a name="uses-for-the-application-model"></a>使用应用程序模型  
 典型的应用程序需要在启动和关闭时执行任务。 例如，当它启动时，应用程序可以显示初始屏幕、 建立数据库连接、 加载已保存的状态，等等。 应用程序关闭时，它可以关闭数据库连接、 保存的当前状态，等等。 此外，应用程序可以执行特定的代码，该应用程序关闭时的情况下，例如在有未经处理的异常。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]应用程序模型，可以轻松创建*单实例*应用程序。 单实例应用程序不同一次可以正常的应用程序中，运行该应用程序只有一个实例。 尝试启动单实例应用程序的另一个实例，将收到通知的原始实例 — 通过`StartupNextInstance`事件，另一次启动尝试所做的。 此通知包括后续实例的命令行参数。 在可以进行的任何初始化之前，应用程序的后续实例之后将关闭。  
  
 单实例应用程序启动并检查它是否为第一个实例或该应用程序的后续实例︰  
  
-   如果是第一个实例，它将正常启动。  
  
-   每个后续尝试启动该应用程序，第一个实例运行时，会导致非常不同的行为。 后续尝试将通知有关命令行参数，第一个实例，并且随后立即退出。 第一个实例句柄`StartupNextInstance`事件，以确定后续实例的命令行参数，然后继续运行。  
  
     下图显示的后续实例发出的第一个实例的信号。  
  
     ![单实例应用程序图像](../../../visual-basic/developing-apps/development-with-my/media/singleinstance.gif "SingleInstance")  
  
 通过处理`StartupNextInstance`事件，您可以控制单实例应用程序的行为方式。 例如，Microsoft Outlook 通常运行作为单实例应用程序;当 Outlook 正在运行并且您尝试启动 Outlook 时同样，焦点转移到原始实例，但不会打开另一个实例。  
  
## <a name="events-in-the-application-model"></a>应用程序模型中的事件  
 应用程序模型中发现下列事件︰  
  
-   **应用程序启动**。 应用程序将引发<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>事件启动时。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup> 通过处理此事件，您可以添加在加载主窗体之前初始化应用程序的代码。 `Startup`事件还提供了取消执行的应用程序在该阶段的启动过程中，如果所需的。  
  
     您可以配置要显示初始屏幕，而应用程序启动代码运行的应用程序。 默认情况下，应用程序模型将取消显示初始屏幕时是`/nosplash`或`-nosplash`使用命令行参数。  
  
-   **单实例应用程序**。 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>单实例应用程序的后续实例启动时引发事件。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance> 该事件传递后续实例的命令行参数。  
  
-   **未经处理的异常**。 如果应用程序时遇到未经处理的异常，它会发出<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>事件。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 您为该事件的处理程序可以检查该异常，并确定是否要继续执行。  
  
     `UnhandledException`在某些情况下，不会引发事件。 有关详细信息，请参阅<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>  
  
-   **网络连接更改**。 如果计算机的网络可用性发生变化，在应用程序引发<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>事件。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>  
  
     `NetworkAvailabilityChanged`在某些情况下，不会引发事件。 有关详细信息，请参阅<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>  
  
-   **应用程序关闭**。 该应用程序提供<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>事件以发出信号时它即将关闭。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown> 该事件处理程序中，您可以确保，操作您的应用程序需要用来执行 — 关闭并保存，例如 — 都已完成。 您可以配置您的应用程序时将关闭主窗体，将其关闭，或若要关闭的情况下仅当所有窗体关闭。  
  
## <a name="availability"></a>可用性  
 默认情况下，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]应用程序模型是适用于 Windows 窗体项目。 如果应用程序配置为使用不同的启动对象，或者具有自定义启动应用程序代码`Sub Main`，则该对象或类可能需要提供的实现<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>类以使用应用程序模型。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 有关更改的启动对象的信息，请参阅[应用程序页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Startup>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.StartupNextInstance>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.Shutdown>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.NetworkAvailabilityChanged>   
 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>   
 [扩展 Visual Basic 应用程序模型](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)
