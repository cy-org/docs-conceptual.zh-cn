---
title: "Windows 窗体和非托管应用程序概述 | Microsoft Docs"
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
  - "COM [Windows 窗体]"
  - "Windows 窗体, 非托管"
  - "COM 互操作"
  - "ActiveX 控件 [Windows 窗体], 关于 ActiveX 控件"
  - "Windows 窗体, 互操作"
ms.assetid: 0a26d99d-8135-4895-8760-c9a2b5f67f14
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体和非托管应用程序概述
Windows 窗体应用程序和控件可以与非托管应用程序进行互操作，但有一些需要注意的问题。 以下各节将介绍 Windows 窗体应用程序和控件支持和不支持的方案和配置。  
  
## Windows 窗体控件和 ActiveX 应用程序  
 由于存在 Microsoft Internet Explorer 和 Microsoft 基础类 \(MFC\) 的异常，因此，在为了托管 ActiveX 控件而设计的应用程序中不支持 Windows 窗体控件。 在能够托管 ActiveX 控件的其他应用程序和开发工具（包括早于 Visual Studio .NET 2003 的 Visual Studio 版本中的 ActiveX 测试容器）中也不支持托管 Windows 窗体控件。  
  
 这些约束还适用于通过组件对象模型 COM 互操作来使用 Windows 窗体控件的情况。 只在 Internet Explorer 中支持通过 COM 可调用包装器 \(CCW\) 来使用 Windows 窗体控件。 有关 COM 互操作的详细信息，请参阅  
  
 [COM 互操作](../Topic/COM%20Interop%20\(Visual%20Basic\).md)。  
  
 下表显示了对 Windows 窗体控件的可用 ActiveX 托管支持。  
  
|Windows 窗体版本|支持|  
|------------------|--------|  
|.NET Framework 版本 1.0|Internet Explorer 5.01 和更高版本|  
|.NET Framework 版本 1.1 和更高版本|Internet Explorer 5.01 和更高版本<br /><br /> Microsoft 基础类 \(MFC\) 7.0 和更高版本|  
  
## 作为 ActiveX 控件托管 Windows 窗体组件  
 在.NET Framework 1.1 中，此支持已扩展到包括 MFC 7.0 和更高版本。 此支持包括与 MFC 7.0 和更高版本的 ActiveX 控件容器完全兼容的任何容器。  
  
 但是，不支持将 Windows 窗体控件注册为 ActiveX 控件。 此外，不支持调用 Windows 窗体控件的 `com.ms.win32.Ole32.CoCreateInstance` 方法。 仅支持对 Windows 窗体控件进行托管激活。 一旦创建了 Windows 窗体控件，即可按与 ActiveX 控件完全相同的方式在 MFC 应用程序上托管它。  
  
 若要在非托管应用程序中使用 Windows 窗体控件，必须使用非托管 CLR 托管 API 来托管 CLR，或使用 C\+\+ 互操作功能。 使用 C\+\+ 互操作功能是建议采用的解决方案。  
  
## COM 客户端应用程序中的 Windows 窗体  
 从 COM 客户端应用程序（例如，Visual Basic 6.0 应用程序或 MFC 应用程序）打开 Windows 窗体时，窗体可能出现意外行为。 例如，当你按 Tab 键时，焦点不会从一个控件更改到另一个控件。 或者当你在命令按钮有焦点的情况下按 Enter 键时，无法引发按钮的 <xref:System.Windows.Forms.Control.Click> 事件。 还可能遇到击键或鼠标操作的其他意外行为。  
  
 发生此行为是因为非托管应用程序没有实现消息循环支持，而 Windows 窗体需要该支持才能正确工作。 COM 客户端应用程序所提供的消息循环根本不同于 Windows 窗体消息循环。  
  
 应用程序的消息循环是内部程序循环，它从线程的消息队列检索消息，然后转换这些消息，之后将它们发送给要处理的应用程序。 Windows 窗体的消息循环与更早的应用程序（例如，Visual Basic 6.0 应用程序和 MFC 应用程序）所提供的消息循环的体系结构不同。 发布到消息循环的窗口消息的处理方式可能与 Windows 窗体期望的不同。 因此，可能发生意外的行为。 某些击键组合可能不起作用，某些鼠标活动可能不工作，或者某些事件可能不会按期望引发。  
  
## 解决互操作性问题  
 可以通过在 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName> 消息循环（它是使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 方法创建的）上显示窗体来解决这些问题。  
  
 若要使 Windows 窗体在 COM 客户端应用程序中正确工作，必须在 Windows 窗体消息循环上运行该窗体。 若要执行此操作，请使用以下方法之一：  
  
-   使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=fullName> 方法显示 Windows 窗体。 有关详细信息，请参阅[如何：通过使用 ShowDialog 方法显示 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)。  
  
-   在新线程上显示每个 Windows 窗体。 有关更多信息，请参见[如何：通过在每个 Windows 窗体各自的线程上显示该 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)。  
  
## 请参阅  
 [Windows 窗体和非托管应用程序](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)   
 [COM 互操作](../Topic/COM%20Interop%20\(Visual%20Basic\).md)   
 [.NET Framework 应用程序中的 COM 互操作性](../Topic/COM%20Interoperability%20in%20.NET%20Framework%20Applications%20\(Visual%20Basic\).md)   
 [COM Interoperability Samples](http://msdn.microsoft.com/zh-cn/09c38567-6380-4d70-848a-e896a4ca05f4)   
 [Aximp.exe（Windows 窗体 ActiveX 控件导入程序）](../../../../docs/framework/tools/aximp-exe-windows-forms-activex-control-importer.md)   
 [向 COM 公开 .NET Framework 组件](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [将 COM 的程序集打包](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)   
 [向 COM 注册程序集](../../../../docs/framework/interop/registering-assemblies-with-com.md)   
 [如何：通过使用 ShowDialog 方法显示 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)   
 [如何：通过在每个 Windows 窗体各自的线程上显示该 Windows 窗体来支持 COM 互操作](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)