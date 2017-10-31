---
title: "如何：通过在每个 Windows 窗体各自的线程上显示该 Windows 窗体来支持 COM 互操作 | Microsoft Docs"
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
  - "COM 互操作, Windows 窗体"
  - "COM [Windows 窗体]"
  - "Windows 窗体, 非托管"
  - "ActiveX 控件 [Windows 窗体], COM 互操作"
  - "Windows 窗体, 互操作"
ms.assetid: a9e04765-d2de-4389-a494-a9a6d07aa6ee
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：通过在每个 Windows 窗体各自的线程上显示该 Windows 窗体来支持 COM 互操作
可通过在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 消息循环上显示窗体来解决 COM 互操作性问题 ，可使用 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName> 方法来创建该消息循环。  
  
 若要使 Windows 窗体在 COM 客户端应用程序上正确工作，必须在 Windows 窗体消息循环上运行该窗体。 若要执行此操作，请使用以下方法之一：  
  
-   使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法显示 Windows 窗体。 有关详细信息，请参阅[如何：通过使用 ShowDialog 方法显示 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)。  
  
-   在单独的线程上显示每个 Windows 窗体。  
  
 在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中，对此功能提供广泛支持。  
  
 另请参阅[演练：通过在每个 Windows 窗体各自的线程上显示该 Windows 窗体来支持 COM 互操作](http://msdn.microsoft.com/library/ms233639\(v=vs.110\))。  
  
## 示例  
 下面的代码示例演示如何在单独的线程上显示窗体，并调用 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName> 方法来启动该线程上的 Windows 窗体消息泵。 若要使用此方法，必须使用 <xref:System.Windows.Forms.Control.Invoke%2A> 方法，封送任何从非托管应用程序对窗体的调用。  
  
 此方法要求窗体上的每个实例通过使用其自身的消息循环在自己的线程上运行。 每个线程上运行的消息循环不能超过一个。 因此，不能更改客户端应用程序的消息循环。 但是，可修改 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 组件以启动使用其自身的消息循环的新线程。  
  
 [!code-vb[System.Windows.Forms.ComInterop#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/COMForm.vb#1)]  
  
 [!code-vb[System.Windows.Forms.ComInterop#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/FormManager.vb#10)]  
  
 [!code-vb[System.Windows.Forms.ComInterop#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ComInterop/VB/Form1.vb#100)]  
  
## 编译代码  
  
-   将 `COMForm`、`Form1` 和 `FormManager` 类型编译成名为 `COMWinform.dll` 的程序集。 使用[将 COM 的程序集打包](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)中所述的一个方法来注册 COM 互操作的程序集。 现在，你可以在非托管应用程序中使用该程序集以及它对应的的类型库 \(.tlb\) 文件。 例如，可在 Visual Basic 6.0 可执行项目中将类型库用作引用。  
  
## 请参阅  
 [向 COM 公开 .NET Framework 组件](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [将 COM 的程序集打包](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)   
 [向 COM 注册程序集](../../../../docs/framework/interop/registering-assemblies-with-com.md)   
 [如何：通过使用 ShowDialog 方法显示 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)   
 [Windows 窗体和非托管应用程序概述](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications-overview.md)